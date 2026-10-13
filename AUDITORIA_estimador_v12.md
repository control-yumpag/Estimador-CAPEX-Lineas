# Auditoría del Estimador CAPEX · Líneas y subestaciones — v11 → v12 (13-oct-2026)

Alcance: reestructuración completa de la presentación del estimador (modo guía por clase, resultado ejecutivo, sustento al final, informe de una página), nueva capa de referencias internacionales y nuevo modelo 3D paramétrico de subestaciones; los motores de cálculo (COES líneas, Osinergmin BDME, COES subestaciones) no cambian. Método: revisión de código, auditoría automática con Playwright (`validacion/audit_v12.js`, 76 comprobaciones: las 61 de v11 más 15 nuevas) y pruebas visuales (capturas de escritorio y móvil, PDF del informe ejecutivo).

Resultado: **76 / 76 comprobaciones superadas en v12**. Sin errores JS en consola. Los valores de E de líneas y subestaciones son idénticos a los de v11 con los mismos datos (la nueva capa solo cambia la presentación y los valores por defecto cuando se cambia de clase o de tensión).

## 1. Hallazgos de la revisión de usabilidad (v11) y cómo se resolvieron

| # | Hallazgo (v11) | Resolución en v12 | Estado |
|---|---|---|---|
| U1 | Demasiada información de entrada: 40–60 campos visibles por espacio (módulo, conductor, mezcla, suelos, allowances, GG&U, indirectos, riesgos, IGV, TC…) antes de ver un número | Modo guía por defecto: la tarjeta «Datos de la estimación» muestra solo lo esencial según la clase (Clase 5: longitud y región; Clase 4: + circuitos, altitud y entorno; Clase 3: + estructura, conductor, vano, mezcla, suelos y accesos; subestaciones: tecnología, alcance, región, celdas, transformadores y potencia, y en Clase 3 configuración de barras, cortocircuito, acople, reactores, celdas MT y área). Todo lo demás toma ratios por defecto y se ve en «Ratios aplicados»; el modo experto conserva el detalle completo | Corregido |
| U2 | Ratios y configuraciones que había que definir a mano (contingencia, riesgos, allowances, fase) sin criterio por clase; al cambiar de tensión en subestaciones se mantenían 50 MVA incluso a 500 kV | Presets por clase (contingencia 45 / 30 / 20 / 12 / 7 %, riesgos 3 / 2.5 / 2 / 1.5 / 1 %, allowances 8+5 / 6+4 / 5+3 / 3+2 / 2+1 %, fase 2 / 2 / 1.5 / 1 / 0.5 %) aplicados a los tres espacios al cambiar de clase; configuración típica por tensión al cambiar de kV en subestaciones (60 kV 25 MVA trifásico · 138 kV 50 MVA · 220 kV 100 MVA · 500 kV 300 MVA en banco monofásico, acople 0 y 63 kA) | Corregido |
| U3 | El resumen mezclaba EDT, donut, ratios, benchmark COES y BIM en una pantalla larga; el número final no destacaba | Pestaña «Resultado»: CAPEX E con S/, IGV y clase; rango esperado por clase (AACE); «Cómo se forma el CAPEX» (barra apilada y seis líneas); «Qué pesa más» (rubros del directo); «Comparación con referencias» (base COES/BDME, mercado peruano e internacional); modelo 3D; «Supuestos clave» y «No incluye». El resumen anterior pasa a «Detalle del estimado» dentro del sustento | Corregido |
| U4 | Trece pestañas al mismo nivel; la gerencia no distingue qué es resultado y qué es sustento | Barra de pestañas en dos niveles: «Resultado» y «Sustento técnico» (detalle, costo directo, metrados, APUs, cotizaciones, diseño, escalamiento, riesgo, bases de datos, referencias, bases, informe) | Corregido |
| U5 | Cabecera con ocho chips técnicos (módulo, base, TC…) | Línea de estado en lenguaje llano («Línea 220 kV doble terna · 60 km · Sierra · Clase 3 · precios 2026 · USD sin IGV»); los chips solo en modo experto | Corregido |
| U6 | No existía un entregable para dirección; la memoria técnica tiene 7–8 páginas | «Informe ejecutivo (1 página)»: total, rango, alcance, barra de formación del CAPEX, tabla, drivers, supuestos, exclusiones, método, comparación con referencias, imagen del modelo 3D y firmas; A4 en una sola página (verificado por PDF en líneas y subestaciones) | Nuevo |
| U7 | Sin referencias internacionales ni criterios de otras guías | Capa INTL: 36 referencias de líneas y 28 de subestaciones (MISO, ACER 2023/2026, CNMC 2015/2026, NEP, IET/PB, CSG 2017/2023, CREG, Banco Mundial, Osinergmin, ProInversión) con valor original, alcance, URL y conversión a USD 2026; franjas comparativas en el resultado y tablas en «Referencias Perú»; clases y contingencias de MISO y AEMO | Nuevo |
| U8 | El visor BIM de torres no tenía sombras ni escala y los conductores eran tramos rectos | Sombras suaves (mapa 2048), figura humana de 1.75 m, conductores en catenaria hacia el medio vano a ambos lados según vano y flecha, botón «Vista» (iso / frente / lateral / planta) y «Girar» en el resultado | Corregido |
| U9 | No había modelo 3D de subestaciones | `sub3d.js`: plataforma, cerco, vías, barras principales y barra alta con pórticos, celdas con equipos (seccionadores, interruptor, TC, TT, pararrayos) por tipo, pórticos de línea, transformadores con radiadores, conservador, bornas, losa, foso y muros cortafuego, edificio de control, sala GIS con módulos y bornas de salida; dimensiones típicas por tensión (ver investigación); vistas, exportación OBJ y comparación del área modelada con el área paramétrica del estimado | Nuevo |
| U10 | La memoria técnica no incluía referencias internacionales | Se mantiene la sección de referencias Perú; las internacionales van en el informe ejecutivo y en la pestaña de referencias | Documentado |

## 2. Verificaciones superadas (v12)

- Las 61 comprobaciones de v11 (cadena A/B/C/E en 9 niveles de línea y 8 subestaciones, Σ paquetes de riesgo = B, PERT, Monte Carlo, escalamiento, informes A/B/C, referencias Perú, proyecto ↔ subestación, visor en pausa, persistencia y móvil) se vuelven a superar sin cambios en los valores.
- **Modo guía**: carga por defecto con la pestaña Resultado, E visible, 11 datos esenciales en Clase 3 (líneas COES), 5 en Clase 4 y 2 en Clase 5; la línea de estado refleja tensión, circuitos, longitud, región y clase.
- **Presets**: Clase 4 escribe cont 30 / riesgo 2.5 / allowances 6+4 / fase 2 en los tres espacios; Clase 5 cont 45; Clase 3 restablece 20 / 2 / 5+3 / 1.5.
- **Proxies**: los datos de la guía escriben en los motores (longitud 75 km, simple terna, conductor) y se sincronizan en sentido inverso.
- **Resultado**: Σ (1 + 2 + 3 + 4 + 5 + D) = E en los tres espacios (tolerancia 1e-9); los rubros de «Qué pesa más» suman entre el 80 y el 100 % del costo directo.
- **Referencias internacionales**: conversión reproducible (ACER 220 kV DC 502,843 € 2023 → 590,491 USD 2026; MISO 230 kV DC 3.3 M$/mi 2024 → 2,164,070 USD/km 2026) y factor de doble circuito de CSG.
- **Informe ejecutivo**: una página A4 con E, clase, rango y exclusiones (líneas y subestaciones).
- **Subestación 3D**: se genera para 60 AIS, 138 GIS, 220 AIS y 500 GIS con tantas celdas como el estimado; la plataforma modelada está entre 0.3 y 3 veces el área paramétrica (0.53–1.05 en las pruebas); configuración típica por tensión al cambiar de kV.
- **BDME**: resultado con E visible, Σ ítems = E y visor BIM montado en el resultado.
- **Modo experto**: muestra los seis grupos del panel y los chips; el modo guía los oculta.

## 3. Observaciones y pendientes

| # | Observación | Estado |
|---|---|---|
| O1 | El modelo 3D de subestación es LOD 200 (geometrías paramétricas, sin conexiones entre equipos ni canaletas); las dimensiones de 500 kV AIS son extrapoladas de 400/765 kV | Documentado |
| O2 | Las tablas Excel de MISO MTEP25/26, AEMO TCD v3, Osinergmin BDME y ANEEL BPR no se pudieron leer; la capa internacional usa los documentos PDF/HTML citados | Pendiente de calibración |
| O3 | Las referencias internacionales son órdenes de magnitud: alcance, terreno, impuestos y contingencia difieren; el estimador lo advierte en cada tarjeta | Documentado |
| O4 | En MT/BT la muestra de mercado (Invierte.pe) mezcla electrificaciones completas; se mantiene el aviso de v11 | Documentado |
| O5 | (v11-H13) Vano por defecto de 33 kV pendiente de validar con el concesionario | Pendiente |

## 4. Archivos de la v12

Nuevos: `parts/guide.js` (modo guía, presets, resultado ejecutivo, informe de una página), `parts/intl.js` + `intl_refs.json` (referencias internacionales), `parts/sub3d.js` (subestación 3D), `validacion/audit_v12.js`, `validacion/shot12.js`, `INVESTIGACION_referencias_v12.md`. Modificados: `parts/body.html`, `parts/body2.html`, `parts/body3.html` (pestañas Resultado / Sustento, paneles ejecutivos, programa de ejecución plegado, pestaña Diseño 3D de subestaciones), `parts/ui.js`, `parts/ui2.js`, `parts/ui3.js` (pestaña por defecto, defaults por tensión en subestaciones), `parts/viewer3d.js` (sombras, catenaria, vistas, escala), `parts/towerlod.js` (conductores en catenaria), `parts/proyecto.js`, `parts/style.css`, `build.py`.
