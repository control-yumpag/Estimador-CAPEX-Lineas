# Estimador CAPEX · Líneas eléctricas (BT / MT / AT / EAT)

Estimador paramétrico de CAPEX para líneas eléctricas del Perú, de 380/220 V a 500 kV, en **USD sin IGV**, publicado con GitHub Pages:

**https://control-yumpag.github.io/Estimador-CAPEX-Lineas/**

Un solo archivo HTML, sin instalación ni internet una vez descargado: bases COES 2025/26 (≥ 138 kV: módulos, APUs, metrados, cotizaciones) y Osinergmin BDME 2025 + kits MT/BT (≤ 60 kV), precios y marcas por componente, escalamiento de la fecha de cotización al periodo de ejecución, riesgo AACE (rangos PERT, mapa de puntos y simulación Monte Carlo beta-PERT), BIM 3D paramétrico de estructuras (Three.js) y memoria de estimación imprimible.

| Archivo | Qué es |
|---|---|
| `index.html` | El estimador (v10, 1-oct-2026). Se abre en el navegador; los datos del proyecto se guardan localmente (localStorage). |
| `AUDITORIA_estimador_v10.md` | Auditoría v9 → v10: hallazgos, correcciones y 37 verificaciones automáticas (Playwright). |
| `NOTAS_v10.md` | Notas de construcción: alcance, método (EDT A = 1 + 2, B = A + 3 + 4, C = B + 5, E = C + D), precios, escalamiento, estructuras, validación, órdenes de magnitud y pendientes. |
| `Estimador_CAPEX_Lineas_fuente_v10.zip` | Código fuente (`capex/parts/`, `build.py`), bases `db.json` / `osi.json`, extracción COES, scripts Osinergmin y pruebas. |
| `Informe_ejemplo_220kV_v10.pdf` | Memoria de estimación de ejemplo (LT 220 kV) generada desde la pestaña «Informe». |
| `Mapa_puntos_PERT_AT_220kV.png` | Captura del mapa de puntos PERT (cómo triangula el método de tres puntos). |

Órdenes de magnitud v10 (precios 2026, monto total de inversión E, USD/km sin IGV): BT rural con alumbrado ≈ 39 k · 10 kV ≈ 29 k · 13.2 kV ≈ 30 k · 22.9 kV ≈ 24 k · 33 kV ≈ 56 k · 60 kV ≈ 110 k · 138 kV ≈ 305 k · 220 kV DT ≈ 421 k · 500 kV ≈ 986 k (los de ≤ 60 kV a 5–25 km; valor regulatorio Osinergmin equivalente ≈ 28 / 21 / 22 / 18 / 41 / 80 k).

Fuentes: COES – módulos de costos de transmisión 2025/26; Osinergmin – Base de Datos de Módulos Estándar (BDME) 2025; LME, BLS CPI-U, INEI; CRU Construction Escalation Index abr-2025; AACE RP 18R-97 / 34R-05 / 42R-08; DGE RD 031-2003-EM. Herramienta de prefactibilidad / factibilidad: no reemplaza metrados de ingeniería, estudio de suelos, trazo definitivo ni cotizaciones firmes.
