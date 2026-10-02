# Auditoría del Estimador CAPEX · Líneas eléctricas — v9 → v10 (1-oct-2026)

Alcance: auditoría integral del estimador (motores COES ≥ 138 kV y Osinergmin BDME ≤ 60 kV), de la carpeta de Drive PRESUPUESTADOR y del método de riesgo (PERT / Monte Carlo), con corrección de hallazgos y entrega de la v10. Método: revisión de código (`engine.js`, `engine2.js`, `ui.js`, `ui2.js`, `escal.js`, `precios.js`, `informe.js`), auditoría automática con Playwright (`validacion/audit_v10.js`, 37 comprobaciones, 9 niveles de tensión), auditoría de datos (`db.json`, `osi.json`) y verificación byte a byte de los archivos subidos a Drive.

Resultado: **37 / 37 comprobaciones superadas en v10** (v9: 15 fallos, de los cuales 4 eran defectos reales del estimador y el resto limitaciones del script inicial). Sin errores JS en consola. Órdenes de magnitud sin cambios respecto a v9 (los hallazgos no alteran el estimado determinístico; solo la simulación y la presentación).

## 1. Hallazgos y correcciones

| # | Severidad | Hallazgo | Evidencia (v9) | Corrección en v10 | Estado |
|---|---|---|---|---|---|
| H1 | Alta | **Edición de rangos Mín/Máx por teclado inoperante.** La tabla de rangos PERT se redibujaba en cada tecla (`oninput` → `renderRiesgo()`): al escribir «−12» el primer carácter «−» se interpretaba como 0, la tabla se reconstruía y el campo perdía el foco. Solo se podían cambiar los rangos con las flechas del control. Afectaba a ambos motores. | Prueba automática: al teclear −12 el valor quedaba en 0 y el foco se perdía (COES y Osinergmin). | El redibujo ocurre al confirmar el valor (`onchange`: Enter, Tab o salir del campo). Prueba: foco conservado al escribir, valor −12 aplicado al confirmar. | Corregido |
| H2 | Alta | **Método inconsistente entre la tabla PERT y la simulación.** La tabla calcula el esperado PERT (Mín + 4·Base + Máx)/6, pero Monte Carlo muestreaba distribuciones **triangulares**, cuya media es (Mín + Base + Máx)/3 y da más peso a las colas. Con los rangos de Clase 3 la contingencia esperada era +5.0 % (PERT) frente a una media simulada de **+10.2 %**: dos cifras de «valor esperado» incompatibles en la misma pestaña. | 220 kV Clase 3: PERT +5.05 % · media MC triangular +10.2 % (2 000 iteraciones). | Nueva distribución **beta-PERT** (λ = 4; muestreo gamma de Marsaglia–Tsang) como opción por defecto, cuya media coincide con el esperado PERT de la tabla; selector «Distribución por paquete» (beta-PERT / triangular) en ambos motores; la triangular queda disponible y documentada. Prueba: media MC beta-PERT +4.9 % ≈ PERT +5.05 %; media MC triangular +10.3 % ≈ (Mín + Base + Máx)/3. | Corregido |
| H3 | Media | **Simulación desactualizada sin aviso.** Al cambiar longitud, clase, precios o rangos después de simular, la pestaña seguía mostrando P10–P90 y «Base (B)» de la corrida anterior; el botón «Usar P80 como contingencia» aplicaba un porcentaje calculado sobre otro estimado. | Código: `state.mc` solo se limpiaba al cambiar la clase. | Aviso ⚠ «Simulación desactualizada: se corrió con B = … y el estimado base actual es …» cuando B difiere > 0.1 %; el botón de simulación regenera los rangos por clase si cambió la clase. | Corregido |
| H4 | Media | **División por cero en la triangular** cuando Mín = Máx (rango 0 / 0): `(m−a)/(b−a)` → NaN y toda la simulación quedaba en NaN. | Revisión de `triangular()`. | `triangular` y `betaPert` devuelven la base cuando Máx ≤ Mín; percentil `P(p)` acotado en [0, N−1]. | Corregido |
| H5 | Baja | KPI «Contingencia PERT» redondeado a 1 decimal («5 %») mientras el botón aplica 5.0: lectura ambigua. | Pantalla Riesgo. | KPI con 2 decimales (5.05 %). | Corregido |
| H6 | Baja | El **informe** no documentaba el análisis de rangos ni la simulación, aunque la contingencia aplicada se justifica con ellos. | `informe.js`. | Nueva sección «Análisis de rangos y contingencia (PERT)» con el mapa de puntos, tabla por paquete (base, mín, máx, esperado, Δ, σ) y la comparación con la contingencia aplicada; impresa en bloque sin corte. | Corregido |
| H7 | Mejora | **Mapa de puntos PERT** (pedido): no existía una vista que explicara cómo se «triangula». | — | Tarjeta «Mapa de puntos · cómo triangula PERT» en la pestaña Riesgo de ambos motores: para cada paquete el triángulo Mín · Base · Máx, el esperado PERT (◆), la media triangular (○), ±σ, fila total con riesgo sistémico y envolvente, y la nube de 400 cuantiles de la simulación con P10 / P50 / P80 / P90 y la media. Eje común en % de desviación respecto a la base. Texto explicativo con las fórmulas y la lectura de la contingencia. En celular se desplaza horizontalmente en vez de encogerse. | Nuevo |
| H8 | Observación | 33 kV por defecto: postes de concreto, 70 mm², vano 300 m → 40.6 k USD/km regulatorio · 55.8 k USD/km (E) a 25 km. Las notas v9 citaban ≈ 69 k a 5 km (mayor peso de costos fijos). Vano típico de 33 kV en postes de 21 m: 150–250 m. | `dbg` v9 = v10 (sin regresión). | Validar el vano por defecto y la familia de postes con el concesionario; no se cambió el valor. | Pendiente de validar |
| H9 | Observación | El módulo de **referencias de mercado Perú** (Invierte.pe + SEACE, `parts/refs.js`, `refs_build.py`) sigue sin integrar: falta completar la extracción de datos de los portales. | ZIP de fuente. | Se mantiene fuera del HTML hasta contar con los datos. | Pendiente |
| H10 | Cosmético | `RISK_DEFAULT` conserva el rango `serv` (servidumbre) aunque la servidumbre está excluida del estimado; `Estimador_CAPEX_LT_COES.html` y `Estimador_CAPEX_Lineas.html` son el mismo archivo con dos nombres. | — | Sin efecto en resultados; se documenta. En Drive y GitHub solo se publica `Estimador_CAPEX_Lineas.html`. | Documentado |

## 2. Verificaciones superadas (v10)

- **Cadena del estimado** en los 9 niveles (BT 0.38 · MT 10 / 13.2 / 22.9 / 33 · AT 60 / 138 / 220 · EAT 500 kV): A = 1 + 2, B = A + 3 + 4, C = B + 5 (5 = % de B), D = % de C, E = C + D, USD/km = E / km.
- **Paquetes de riesgo**: la suma de las bases de los paquetes reproduce exactamente B en ambos motores (tolerancia 1e-6), de modo que la contingencia PERT y la simulación se expresan sobre el mismo estimado base.
- **Tabla PERT**: fila «Estimado base (B)» = B; esperado total = Σ (Mín + Máx + 4·Base)/6 × fSys, con fSys = (2 + lo + hi + 4)/6 del riesgo sistémico.
- **Escalamiento**: Σ montos por grupo = ítem 3; Σ pesos A_g = A; Σ pesos por año = 1; con año de precios 2028 el factor de actualización de cotizaciones es > 1 y el escalamiento a la ejecución disminuye (5.63 % → menor), como corresponde al mover la fecha base hacia la ejecución.
- **Monte Carlo**: P10 ≤ P50 ≤ P90, base = B; media beta-PERT ≈ esperado PERT; media triangular ≈ (Mín + Base + Máx)/3.
- **Informe** A y B: muestran el E del estimado; nueva sección PERT; PDF A4 generado sin errores.
- **Exportación JSON** (programa, escalamiento, precios) disponible.
- **Persistencia** (modo y kV tras recargar) y **móvil** (390 px sin desplazamiento horizontal de página).
- **Datos**: 48 módulos COES (500 kV: 9 · 220 kV: 17 · 138 kV: 9 · 60 kV: 13) sin campos faltantes ni valores nulos en km, vano, estructuras, partidas 1.1–5.0 y USD/km; 34 cotizaciones de conductores; 62 módulos BDME, 826 precios I-402/I-403, kits MT/BT/SED/AT.

## 3. Auditoría de la carpeta de Drive (PRESUPUESTADOR)

Los archivos subidos el 1-oct-2026 coinciden byte a byte en tamaño con los locales: `Estimador_CAPEX_Lineas.html` 2 317 406 B (v9), `Estimador_CAPEX_Lineas_fuente_v9.zip` 4 310 198 B, `Informe_ejemplo_220kV_v9.pdf` 245 962 B, `Notas_construccion_v9.md` 13 210 B y 12 PNG en `Capturas/`; Google Docs LEEME y Notas creados con el conector. En esta entrega se reemplazan el HTML y el ZIP por la **v10**, se añaden este informe, el informe PDF de ejemplo v10 (con la sección PERT) y las capturas del mapa de puntos, y se actualiza el LEEME.

## 4. Cómo leer el mapa de puntos PERT

1. Cada paquete tiene tres puntos: **Mín** (optimista, azul), **Base** (más probable = moda, gris, en 0 %) y **Máx** (pesimista, rojo). El triángulo sombreado es la distribución implícita.
2. El **esperado PERT** (◆ naranja) = (Mín + 4·Base + Máx)/6: pondera la moda cuatro veces. Como los rangos son asimétricos hacia el alza, cae a la derecha de la base; esa distancia (en % y USD, a la derecha de cada fila) es la contingencia esperada del paquete. σ = (Máx − Mín)/6 se dibuja como barra ±σ.
3. La **media triangular** (○) = (Mín + Base + Máx)/3 queda más a la derecha porque da el mismo peso a los tres puntos: por eso una simulación triangular «infla» la contingencia frente a PERT (H2).
4. La fila **Estimado base (B)** suma los paquetes y aplica el riesgo sistémico (× fSys); su envolvente Mín/Máx es el caso extremo, no una distribución.
5. La **nube de puntos** de la simulación (400 cuantiles) muestra cómo se distribuye B al sumar paquetes muestreados de forma independiente; P80 − B es la contingencia recomendada a P80.

## 5. Archivos de la v10

`parts/pertmap.js` (nuevo), `parts/engine.js` (beta-PERT, gamma, triangular segura, `monteCarlo(pk, ranges, N, dist)`), `parts/ui.js`, `parts/ui2.js` (edición de rangos, aviso de simulación desactualizada, selector de distribución, mapa), `parts/body.html`, `parts/body2.html` (selector y tarjeta del mapa), `parts/informe.js` (sección PERT), `parts/style.css` (`.pert-wrap`), `build.py`, `validacion/audit_v10.js`, `validacion/shot_pert.js`.
