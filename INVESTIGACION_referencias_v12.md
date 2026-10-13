# Investigación de referencias para el Estimador CAPEX v12 (13-oct-2026)

Resumen de la investigación web realizada para reestructurar el estimador: cómo se organizan los estimadores profesionales (Cleopatra Enterprise y otros), qué dicen las guías de clasificación de estimados, costos unitarios públicos de líneas y subestaciones en EE. UU., Europa, China, Australia, Latinoamérica y Perú, estructuras y porcentajes de los reguladores de la región, y dimensiones típicas de subestaciones para el modelo 3D. Solo se usaron cifras leídas en las fuentes citadas; las conversiones a USD 2026 del estimador son aproximadas (tipo de cambio del año de la fuente y CPI-U).

## 1. Patrones de los estimadores profesionales (lo que se adoptó en v12)

| Patrón | Fuente | Cómo se aplicó en v12 |
|---|---|---|
| El total siempre acompañado de la clase AACE y su rango de precisión; la clase la define la madurez de la definición del proyecto | AACE 18R-97 / PGD-01; BC Cost Estimating Guidance | Tarjeta «Rango esperado para la Clase X» junto al CAPEX; chip de clase en la cabecera |
| Escalera base → contingencia → esperado → total; la contingencia es una línea aparte y nunca se deriva de la clase | NZTA estimate template; DOE G 413.3-21A; Cleopatra (riesgo) | Barra apilada 1 · 2 · 3 · 4 · 5 · D = E y tabla de seis líneas |
| Estructura de costos de primer nivel: directos, indirectos, escalamiento, contingencia | Cleopatra (CBS) | Buckets del resultado ejecutivo |
| Biblioteca de costos separada del estimado y métodos por clase (factor/paramétrico Clase 5-4, cantidades Clase 3, precios unitarios Clase 2) | Cleopatra Enterprise (CESK, técnicas); ACCE | Datos esenciales por clase; módulos COES/BDME como biblioteca; modo experto para Clase 2 |
| Asistente con pocos parámetros + multiplicadores de contexto (terreno, urbano, altitud) | AEMO TCD; MISO; WECC/B&V | Región, altitud, entorno, accesos, suelos como únicos modificadores en modo guía |
| Tableros por rol: ejecutivos ven KPI y rango; el PM ve WBS y detalle | Cleopatra dashboards; GAO paso 11 | Pestaña «Resultado» y «Sustento técnico» |
| Benchmarking normalizado (moneda, ubicación, inflación, alcance) por unidad ($/km, $/bahía, $/MVA) | Cleopatra (benchmarking); AEMO | Tarjeta «Comparación con referencias» y pestaña «Referencias Perú» con tablas internacionales |
| Drivers de costo visibles (top 5) y sensibilidad | GAO; CostOS what-if | Tarjeta «Qué pesa más» |
| Supuestos y exclusiones visibles con el total; informe de una página | AACE 34R-05 (BoE); NZTA | Tarjetas «Supuestos clave» / «No incluye» e «Informe ejecutivo (1 página)» |

Cleopatra Enterprise (Cost Engineering Consultancy): módulos de estimación, CESK (biblioteca de más de 1.5 millones de ítems y 2,000 proyectos), control de proyectos, riesgo, dashboards, portafolio y BIM; estructuras de desglose flexibles (WBS/CBS), comparación entre estimados, técnicas de factor (regla 0.6, Hand), paramétricas, por cantidades y por precios unitarios ligadas a las clases AACE; benchmarking normalizado; contingencia como rango (P50 dueño / P85 contratista). No se encontraron funciones de IA de producto documentadas públicamente (solo un «motor inteligente de importación» de BoQ/MTO y «modelos de costo inteligentes»). Fuentes: https://cleopatraenterprise.com/cost-estimating-software/ · https://cleopatraenterprise.com/cesk-data/ · https://cleopatraenterprise.com/blog/5-cost-estimation-techniques-of-cleopatra-enterprise-software/ · https://cleopatraenterprise.com/blog/cost-benchmarking-in-capital-projects/ · https://cleopatraenterprise.com/project-risk-management-software/

Otras herramientas revisadas: Aspen Capital Cost Estimator (un modelo de concepto a detalle, clases IV–II, Monte Carlo, ACCE Insights), CostOS (what-if, histórico, CosMO para benchmarking), Sage Estimating (totals page templates, alternates), Oracle Unifier (presupuesto por CBS), EPRI (guía y libro Excel de costos de transmisión), WECC/B&V (calculadora Excel con multiplicadores de terreno 1.00 llano · 1.05 desierto · 1.40 colinas · 1.75 montaña · 2.25 bosque · 1.59 urbano), MISO (guía anual con tablas por kV).

## 2. Clases de estimado y contingencia

| Clase | Definición | Uso | Precisión (AACE 18R-97 y 96R-18) | Contingencia MISO | Riesgo desconocido AEMO/GHD 2025 |
|---|---|---|---|---|---|
| 5 | 0–2 % | Idea / tamizaje | −20…−50 % / +30…+100 % | 30 % (exploratorio) | 5b 30 % (±50 %) · 5a 15 % (±30 %) |
| 4 | 1–15 % | Prefactibilidad | −15…−30 % / +20…+50 % | 20 % (planeamiento) | 9 % (±20 %) |
| 3 | 10–40 % | Autorización de presupuesto | −10…−20 % / +10…+30 % | 15 % (alcance) | 4 % (±10 %) |
| 2 | 30–75 % | Control / licitación | −5…−15 % / +5…+20 % | — | 0 % (±5 %) |
| 1 | 65–100 % | Verificación | −3…−10 % / +3…+15 % | — | 0 % (±5 %) |

- AACE 96R-18 es la clasificación aplicada a líneas de transmisión (> 100 kV; mismas bandas que 18R-97, metodología por costo/longitud). 97R-18 corresponde a ductos, no a subestaciones; las subestaciones se clasifican con 18R-97. Fuentes: https://web.aacei.org/docs/default-source/toc/toc_18r-97.pdf · https://web.aacei.org/docs/default-source/toc/toc_96r-18.pdf · https://library.aacei.org/pgd01/pgd01.shtml
- DOE G 413.3-21A: CD-0 = Clase 5, CD-1 = Clase 4, CD-2 = Clase 3; los rangos de clase no deben usarse para calcular la contingencia. https://www.energy.gov/documents/doe-2018-cost-est-guide
- MISO MTEP21/24/25: contingencia 30 / 20 / 15 % según nivel de definición y AFUDC 7.5 %; escalamiento MTEP25 4 % anual (estructuras 6 %, equipos/conductor/OPGW 8 %). https://interchange.puc.texas.gov/Documents/53601_1_1208306.PDF · https://cdn.misoenergy.org/20240501%20PSC%20Item%2004%20MISO%20Transmission%20Cost%20Estimation%20Guide%20for%20MTEP24632680.pdf
- AEMO/GHD Transmission Cost Database 2025: línea base sin riesgos + riesgos conocidos y desconocidos por clase; indirectos 10–16 %. https://aemo.com.au/-/media/files/stakeholder_consultation/consultations/nem-consultations/2025/2025-electricity-network-options-report/ghd-2025-transmission-cost-database-update-final-report
- Exponentes de capacidad (regla 0.6): AACE 59R-10 (0.5–0.85 típico; método de Clase 5/4); Towler & Sinnott; no existe un exponente publicado verificado para transformadores (CLASP 25/63/100 MVA implica ≈ 0.5). El estimador mantiene 0.55 (transformadores) y 0.6 (reactores) solo como interpolación entre módulos COES vecinos.

Los ratios por defecto del estimador (plantilla LE2): contingencia 45 / 30 / 20 / 12 / 7 % de B para Clases 5–1, provisión por riesgos 3 / 2.5 / 2 / 1.5 / 1 % de A, allowances 8+5 / 6+4 / 5+3 / 3+2 / 2+1 %, costo de fase 2 / 2 / 1.5 / 1 / 0.5 % de C. Están dentro de los rangos de la compañía y por encima de MISO/AEMO para Clase 3, lo que se explica al usuario en la tarjeta de ratios.

## 3. Costos unitarios de líneas (valores originales)

| Región · fuente | Ítem | Valor | Moneda / año | Alcance |
|---|---|---|---|---|
| EE. UU. · MISO MTEP24 | 138 kV SC / DC | 1.9–2.3 / 2.8–3.3 M$/mi | USD 2024 | Incluye terreno, permisos, PM 5.5 %, A&G 1.5 %, ingeniería 3 %, impuestos, contingencia 30 % y AFUDC 7.5 % |
| | 230 kV SC / DC | 2.0–2.6 / 3.3–4.0 M$/mi | | |
| | 345 kV SC / DC · 500 kV SC · 765 kV SC | 3.2–4.1 / 5.5–6.4 · 4.1–5.1 · 5.2–6.3 M$/mi | | |
| EE. UU. · ERCOT 2024 | 345 kV DC · 138 kV · 765 kV SC | 4.04 · 2.5 · 6.10 M$/mi | USD, año n. d. | Estimados genéricos |
| Europa · ACER UIC 2023 | 220 kV SC / DC | 362,180 (IQR 303–543 k) / 502,843 (442–673 k) €/km | EUR 2023 | Costos realizados, sin impuestos, ≥ 5 km |
| | 400 kV SC / DC · 110–150 kV DC | 396,856 / 1,050,044 · 259,718 €/km | | |
| Europa · ACER UIC 2026 | 220 kV SC / DC · 400 kV SC / DC | 0.40 / 0.53 · 0.52 / 1.18 M€/km (medianas) | EUR, datos 2025-26 | Proyectos en servicio |
| España · CNMC Circular 7/2025 (desde 2026) | 400 kV dúplex SC / DC · 220 kV dúplex SC / DC · 220 kV simplex SC | 339,622 / 574,744 · 309,045 / 523,001 · 287,413 €/km | EUR | Valores regulatorios sin costos financieros; Orden 2015: 298,437 / 505,047 · 266,617 / 451,197 |
| Alemania · NEP 2037/2045 | 380 kV DC nueva traza · HTLS · cable 380 kV | 4.5 · 4.7 · 16 M€/km | EUR, n. d. | Estimación de los TSO |
| Reino Unido · IET/PB 2012 | 400 kV 2×3,190 MW | 1.6–1.7 £M/km | GBP 4T-2011 | Solo obra, PM 10 % y contingencia 10 % |
| China · CSG 2023 | 110 / 220 / 500 kV SC | 1.25 / 1.52–2.11 / 2.76–3.64 M CNY/km | CNY 2023 | Cuerpo de obra estático; DC × 1.7 / 1.8 / 2.0 |
| Colombia · CREG 011/2009 | 230 kV SC / DC · 500 kV SC | 285,994 / 421,565 · 583,314 miles COP/km | COP dic-2008 | Unidades constructivas, sin terreno ni servidumbre; > 2,000 msnm 338,089 |
| Global · Banco Mundial 2026 | 220–230 kV SC / DC · 500 kV SC / DC | 0.216→0.596 / 0.326→0.996 · 0.281→1.221 / 0.646→1.427 M$/km | USD 2010 | Proyectos BM → literatura; +12 % > 2,500 msnm, +15 % montañoso, monoposte +45 %, < 5 km +50 % |
| Perú · Osinergmin PI 2025-29 | 60 / 138 / 220 kV | 0.093 / 0.100 / 0.121 M$/km | USD 2023 (BDME) | Módulos de planificación (≈ 3–14 veces por debajo de ACER/MISO) |
| Perú · ProInversión 2023 | 500 kV Huánuco–Trujillo (662 km) | US$ 561 M ≈ 0.85 M$/km | USD 2023 | Incluye 2 SE nuevas y 2 ampliaciones |
| Perú · COES vs concesionario | SE Poroma / SE San José | +12.9 % / +23.6 % | — | Brecha anteproyecto COES → estimado del concesionario (informe 192-2025-GRT) |

## 4. Costos unitarios de subestaciones (valores originales)

| Región · fuente | Ítem | Valor | Moneda / año |
|---|---|---|---|
| MISO MTEP24 | Posición adicional (anillo) 138 / 230 / 345 / 500 kV | 1.7 / 2.2 / 3.4 / 5.3 M$ (con contingencia 30 % y AFUDC) | USD 2024 |
| | Transformador 138/69 · 230/115 · 345/138 · 500/230 kV | 5,050 · 5,896 · 6,880 · 8,884 $/MVA | USD 2024 |
| | Interruptor (solo material) 138 / 230 / 345 / 500 kV | 62,332 / 112,791 / 373,398 / 491,531 $ | USD 2024 |
| ACER 2023 | Bahía 220–275 kV · 380–400 kV | 1,133,288 · 2,435,831 € (mediana) | EUR 2023 |
| | Transformador 220/66 · 400/110 · 400/220 kV | 1.59 · 4.35 · 3.85 M€/unidad | EUR 2023 |
| ACER 2026 | SE completa 0–5 / 6–9 / 10–60 bahías · trafo 220/50 · 400/220 | 4.60 / 11.27 / 27.03 M€ · 1.68 · 6.96 M€ | EUR |
| CNMC 2026 | Posición 400 kV convencional / GIS · 220 kV IM / otras / GIS | 1,075,226 / 2,311,560 · 706,083 / 751,256 / 1,524,699 € | EUR |
| Orden IET/2659/2015 | Transformador 400/220 · reactancia · condensador | 9,835 €/MVA · 15,499 €/MVAr · 19,613 €/MVAr | EUR 2015 |
| NEP 2023 | Bahía de línea 220 / 380 kV · de trafo 220 / 380 · transformador | 3.5 / 4.4 · 3.3 / 4.9 M€ · 0.015–0.021 M€/MVA | EUR |
| CSG 2017 | SE nueva 110 kV 2×50 · 220 kV 2×180 · 500 kV 2×1000 MVA | 370 · 252 · 125 CNY/kVA | CNY 2017 |
| CREG 2009 | Bahía de línea 230 kV BS / DB / IM / GIS · 500 kV DBT · banco 500/230 450 MVA | 2,235 / 2,465 / 2,569 / 5,406 · 6,428 · 18,004 M COP | COP dic-2008 |
| Osinergmin 2024 | Nueva SET Chocope (138 kV) | US$ 5.96 M | USD (BDME 2023-24) |

## 5. Cómo arman el estimado los reguladores de la región

- **Perú (Osinergmin BDME)**: catálogo de módulos estándar con código autoexplicativo; precios de aduanas, facturas y contratos actualizados cada año; GG 10 % + utilidad 10 % sobre obras civiles y montaje; administración, supervisión y financieros sobre la parte en soles; ingeniería de detalle 3.86 % en centro de control; interés intercalario 0.47–0.54 %; servidumbres fuera de los módulos de línea; IGV no recuperable reconocido al 100 %; factor Amazonía 1.0620 (Res. 152-2026-OS/CD). Nueva BDME en consulta (Res. 034-2026-OS/CD). Fuentes: https://busquedas.elperuano.pe/dispositivo/NL/2560040-1 · https://busquedas.elperuano.pe/dispositivo/NL/2537944-1 · https://www.osinergmin.gob.pe/Resoluciones/pdf/2026/Informe-Tecnico-487-2026-GRT.pdf
- **Colombia (CREG)**: unidades constructivas cerradas (líneas por km según circuitos y altitud; bahías por configuración + módulo común), valores fijados por resolución; terrenos y servidumbres aparte; AOM 3.1–3.8 % del costo de reposición; actualización 2024 (ISES) con base de 1,459 registros y mediana con filtro de atípicos. https://gestornormativo.creg.gov.co/gestor/entorno/docs/resolucion_creg_0011_2009.htm
- **Brasil (ANEEL)**: Banco de Preços de Referência con módulos paramétricos por longitud, tensión, circuitos, estructura y cable, precios por región y actualización mensual; BDI de obras eléctricas 24–28 % (TCU). https://dadosabertos.aneel.gov.br/dataset/bpr-banco-de-precos-de-referencia-linha-de-transmissao
- **Chile (CNE)**: VI = [Cu·(1+Fl+B)+MO]·(1+Ing+Gg)·(1+Int)+BI+CE con recargos por familia (paños por kV, transformadores por MVA, líneas por tramo de longitud); sin utilidad ni contingencia explícitas. https://www.cne.cl/wp-content/uploads/2024/03/Informe-Tecnico-Definitivo-Art.52%C2%B0-Reglamento.pdf
- **España (CNMC)**: valores unitarios por instalación tipo derivados de costos auditados; término fijo para líneas < 10 km; factores de 80 % (primer circuito con apoyos para dos) y 30 % (segundo circuito); desviación real/unitarios −8.5 % (2018-23) a +10.8 % (2024). https://www.boe.es/diario_boe/txt.php?id=BOE-A-2025-26676 · https://www.cnmc.es/sites/default/files/6205162.pdf
- Ningún regulador publica rangos: todos dan valores puntuales; las únicas bandas empíricas son las desviaciones real/referencia (CNMC, COES).

## 6. Dimensiones típicas de subestaciones usadas en el modelo 3D

| Parámetro | 60–72.5 kV | 138–145 kV | 220–245 kV | 500–550 kV |
|---|---|---|---|---|
| Ancho de bahía AIS | 8 m | 10.5 m | 16 m | 28 m (est.) |
| Separación de fases en barra | 2.0 m | 2.75 m | 4.0 m | 7.5 m (est.) |
| Barra baja / barra alta / pórtico | 4.0 / 6.0 / 9 m | 4.7 / 7.5 / 11 m | 5.75 / 10.5 / 15 m | 10 / 18 / 27 m (est.) |
| Largo de bahía doble barra / diámetro 1½ | 20 / 40 m | 28 / 50 m | 40 / 75 m | 55 / 120 m |
| Altura total CB / CT / VT / seccionador | 4.65 / 4.3 / 4.2 / 3.6 m | 5.2 / 4.6 / 4.6 / 4.4 m | 6.7 / 5.6 / 5.7 / 5.2 m | ≈ 9.5 / 8.5 / 8.6 / 7 m |
| Bahía GIS / luz de sala | 0.8–0.9 / 10 m | 1.0 / 11 m | 1.5 / 12 m | 3.1 / 14.5 m |
| Transformador (L×A×H) | 6.5×4×5 m (≤ 30 MVA) | 6.5×4×5 m | 8.5×6.6×7.5 m (100 MVA) | 3 monofásicos 8×5×7.2 m |
| Edificio de control | ≈ 150 m² | ≈ 200 m² | ≈ 250 m² | ≈ 700 m² |
| Cerco | 2.4 m + alambre de púas | idem | idem | 2.5 m + púas |

Áreas empíricas: AIS 220 kV ≈ 1,870–2,150 m² por posición (SEA Chile: 3.55 ha / 19 posiciones); 500 kV ≈ 6,400 m² por posición (JICA); GIS ≈ 21–23 % del AIS a 400–500 kV, híbrido ≈ 48 %. Fuentes: Energy Queensland STNW3013 (https://swp.energex.com.au/upload/technical_documents/20240115_104427_919.pdf), SEA Chile (https://firma.sea.gob.cl/publicaciones/3b/34/2145470552.pdf), BHEL/REC-PDCL, Siemens 8DN9/8DQ1, Hitachi ELK, EirGrid AIS vs GIS (https://www.eirgrid.ie/sites/default/files/publications/Appendix%20B%20Technical%20Comparison%20of%20AIS%20vs.GIS%20Substation%20Opt.pdf), JICA/Kansai (https://openjicareport.jica.go.jp/pdf/11915303_08.pdf), AXA XL PRC.5.9.2 (separación entre transformadores y muros cortafuego).

## 7. Advertencias para comparar

1. MISO incluye contingencia 30 % y AFUDC 7.5 % (dividir entre 1.3975 para llevar a base), terreno, permisos e impuestos; AEMO incluye servidumbre y compensaciones ambientales; CREG y Osinergmin excluyen terreno y servidumbre; CNMC excluye costos financieros; ACER exige costos sin impuestos.
2. Años base distintos (USD 2024, EUR 2023/2025, AUD 2024/25, USD 2010, GBP 2011, COP 2008, CNY 2017/2023): el estimador escala con CPI-U y lo declara en cada tabla.
3. ACER y Banco Mundial son costos realizados; MISO, AEMO y CSG son estimados o topes de control; CNMC, CREG y Osinergmin son valores de remuneración o planificación.
4. Las tablas de módulos por kV de MISO MTEP25/26, AEMO TCD v3, Osinergmin BDME y ANEEL BPR son planillas Excel que no se pudieron leer en esta sesión; conviene descargarlas a mano para una futura calibración.
