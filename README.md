# Estimador CAPEX · Líneas eléctricas y subestaciones (Perú)

Estimador paramétrico de CAPEX en **USD sin IGV** para **líneas** de 380/220 V a 500 kV (BT / MT / AT / EAT) y **subestaciones** de 60, 138, 220 y 500 kV (AIS y GIS), publicado con GitHub Pages:

**https://control-yumpag.github.io/Estimador-CAPEX-Lineas/**

Un solo archivo HTML, sin instalación ni internet una vez descargado.

## Cómo se usa (v12)

1. **Modo guía** (por defecto): elige el tipo de obra (línea / subestación), la tensión y la **clase de estimado** (AACE 18R-97 / 96R-18). La tarjeta «Datos de la estimación» pide solo lo esencial según la clase: Clase 5 longitud y región; Clase 4 + circuitos, altitud y entorno (o tecnología, alcance y potencia en subestaciones); Clase 3 + estructura, conductor, vano, mezcla de estructuras, suelos y accesos (o configuración de barras, cortocircuito, acople, reactores, celdas MT y área). Todo lo demás usa ratios por defecto según la clase (contingencia 45 / 30 / 20 / 12 / 7 %, riesgos, allowances, fase) que se listan en «Ratios aplicados».
2. **Resultado**: CAPEX del proyecto (E) con su rango por clase, cómo se forma (directo, indirecto, escalamiento, riesgos, contingencia, fase), qué pesa más, comparación con la base COES/BDME, el mercado peruano (Invierte.pe, SEACE) y referencias internacionales (MISO, ACER, CNMC, NEP, CSG, CREG, Banco Mundial), modelo 3D, supuestos y exclusiones. Botón **«Informe ejecutivo (1 página)»** para dirección y **«Memoria técnica»** completa.
3. **Sustento técnico**: detalle del estimado, costo directo, metrados, APUs, cotizaciones, diseño (torre y planta; subestación 3D), escalamiento, riesgo y contingencia (PERT, Monte Carlo, mapa de puntos), bases de datos, referencias Perú e internacionales, bases del estimado e informe.
4. **Modo experto** (botón en la cabecera): todos los parámetros editables (módulos, precios y marcas, GG&U, indirectos, riesgos, escenarios).

| Archivo | Qué es |
|---|---|
| `index.html` | El estimador (v12, 13-oct-2026). Los datos del proyecto se guardan localmente (localStorage). |
| `AUDITORIA_estimador_v12.md` | Auditoría v11 → v12: hallazgos de usabilidad, resolución y 76 verificaciones automáticas (Playwright). |
| `INVESTIGACION_referencias_v12.md` | Investigación: estimadores profesionales (Cleopatra, ACCE, CostOS…), clases AACE / MISO / AEMO, costos unitarios de EE. UU., Europa, China, Australia, Latinoamérica y Perú, reguladores de la región y dimensiones de subestaciones. |
| `NOTAS_v12.md` | Notas de construcción: método (A = 1 + 2, B = A + 3 + 4, C = B + 5, E = C + D), bases de datos, ratios por clase, órdenes de magnitud y pendientes. |
| `Estimador_CAPEX_fuente_v12_codigo.zip` (código, bases y pruebas) y `Estimador_CAPEX_fuente_v12_extracciones.zip` (extracción cruda COES, módulos de subestaciones, Invierte.pe/SEACE y capturas) | Código fuente (`capex/parts/`, `build.py`), bases `db.json`, `osi.json`, `se_db.json`, referencias `refs.json`, `refs_se.json`, `intl_refs.json`, extracciones y pruebas. |
| `Informe_ejecutivo_LT_220kV_v12.pdf`, `Informe_ejecutivo_SE_220kV_v12.pdf` | Informes ejecutivos de una página de ejemplo. |
| `01_Resultado_linea_220kV.png`, `07_Resultado_subestacion_138kV.png`, `09_Subestacion_3D_138kV_AIS.png` | Capturas. |
| `Informe_ejemplo_220kV_v10.pdf`, `AUDITORIA_estimador_v11.md`, `NOTAS_v11.md`, `Estimador_CAPEX_fuente_v11.zip` | Versiones anteriores. |

Órdenes de magnitud (precios 2026, CAPEX E sin IGV, Clase 3): líneas BT rural ≈ 39 k · 10 kV ≈ 29 k · 13.2 kV ≈ 30 k · 22.9 kV ≈ 24 k · 33 kV ≈ 56 k · 60 kV ≈ 110 k · 138 kV ≈ 305 k · 220 kV DT ≈ 421 k · 500 kV ≈ 986 k USD/km; subestaciones nuevas (2 L + 2 T + 1 A, 1 transformador) 60 kV AIS ≈ 11 M · 138 kV ≈ 17 M · 220 kV ≈ 24 M · 500 kV ≈ 47 M USD. Referencias internacionales llevadas a USD 2026: 220 kV doble circuito ≈ 0.49 M (CSG China) · 0.59 M (ACER Europa) · 0.58 M (CNMC España) · 2.2–2.6 M (MISO EE. UU., con contingencia 30 % y AFUDC) por km.

Fuentes: COES – Base de Datos de Costos de Sistemas de Transmisión 2025/26; Osinergmin – BDME 2025; MEF – Invierte.pe; OECE – SEACE 3.0; MISO MTEP24; ACER UIC 2023/2026; CNMC Circular 7/2025; NEP 2023; China Southern Grid 2017/2023; CREG 011/2009; Banco Mundial/ESMAP 2026; AACE RP 18R-97 / 34R-05 / 42R-08 / 59R-10 / 96R-18; DOE G 413.3-21A; AEMO/GHD TCD 2025. Herramienta de prefactibilidad / factibilidad: no reemplaza metrados de ingeniería, estudio de suelos, trazo definitivo ni cotizaciones firmes.
