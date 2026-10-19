# GAC · Auditoría del Proceso Analítico

Repositorio de auditoría del proyecto de analítica comercial de **GAC Motor — Plaza Angelópolis** (socio formador: Grupo Autos del Centro).
Agrupa en un solo lugar, organizado por etapa, todo el proceso: **datos crudos, datos limpios, notebooks de cada etapa, documentos entregables y código del dashboard**.

**Dashboard desplegado (producto final):** https://dashboard-gac-53x7ncfkmh6t2yk75k7cmf.streamlit.app
**Repo de despliegue del dashboard:** https://github.com/a01736195-bot/Dashboard-GAC

> Este repo es para **auditar el proceso**; el repo de despliegue es el que mantiene la app en vivo.

---

## 1. Mapa del proceso

```
Fuente cruda (exportaciones del Excel maestro de la plaza, 7 ago 2026)
        │  data/raw/  — 21 hojas en CSV + 2 xlsx sin outliers
        ▼
ETAPA I · Limpieza e integración ────────────────► notebooks/etapa1_limpieza/
        │  salida: data/  (9 CSVs depurados)
        ▼
ETAPA II · Modelado predictivo ──────────────────► notebooks/etapa2_modelado/
  · Correlaciones, regresión lineal simple y múltiple
  · Regresión del embudo
  · Regresión logística (PDM y Ventas, con balanceo)
        │
        ▼
ETAPA III · ANOVA ───────────────────────────────► notebooks/etapa3_anova/
  · Citas Digital por agente BDC
  · Marketing por canal · Plazas
        │
        ▼
PRODUCTO · Dashboard Streamlit ──────────────────► app/  (app.py + vistas_modelos.py)
  5 vistas: Panorama, Embudo, Desempeño,
  Modelos Predictivos y Laboratorio
```

## 2. Estructura del repositorio

| Carpeta | Contenido |
|---|---|
| `data/raw/` | **Fuente cruda**: 21 hojas del Excel maestro "Analisis GAC Full 7 agosto 2026" exportadas a CSV, más `Ventas_por_Asesor_sin_outliers.xlsx` y `Analisis_de_Piso_sin_outliers.xlsx` |
| `data/` | Los 9 CSV **depurados** que alimentan el dashboard y los modelos |
| `notebooks/etapa1_limpieza/` | `Pipeline GAC - Entregable 1.ipynb` · `Analisis_GAC_Limpieza_Graficos.ipynb` |
| `notebooks/etapa2_modelado/` | `Regresiones_GAC_Full.ipynb` (carga las 7 bases) · `Regresion_Simple_Resumen.ipynb` · `regresion_lineal_simple.ipynb` · `Regresion_Logistica_Binaria_Resumen.ipynb` (Ventas) · `reglog_e5.ipynb` (PDM con oversampling) |
| `notebooks/etapa3_anova/` | `ANOVA_Marketing_GAC.ipynb` · `Copia de Despliegue_ANOVA.ipynb` |
| `notebooks/exploracion/` | `analisis_GAC_oficial.ipynb` · `codigos.ipynb` (exploraciones previas) |
| `notebooks/` | `DASHBOARD_GAC.ipynb` — análisis univariado + regresión (despliegue) |
| `docs/` | Entregables: reporte de solución, propuestas y presentaciones (ver §4) |
| `app/` | Código del dashboard: `app.py`, `vistas_modelos.py`, tema, requirements y versión original por etapas (`archivo/`) |

## 3. Diccionario de datos

### 3.1 Crudos (`data/raw/`)

Hojas del libro maestro de la plaza: `SDC`, `Resumen`, `Citas Digital`, `Ventas por Asesor`, `Ventas`, `Analisis de Piso`, `Base de Leads`, `Base de Tlaxcala`, `Plazas`, `Funnel`, `Marketing`, `MKT Digital`, `Leads por Canal`, `Principales Canales`, `CPL FACEBOOK`, `Conversaciones por Asesor`, `TOPS MKT`, `TOPS POST VENTA`, `TOPS TDH`, `TOPS VENTAS`, `BCS`.

### 3.2 Depurados (`data/`)

| Archivo | Filas × cols | Qué contiene | Usado en |
|---|---|---|---|
| `Bitacora_Piso_Limpia.csv` | 197 × 11 | Bitácora de piso: fecha, cliente, asesor, estatus del lead | Desempeño · Asesores |
| `Citas_Digital.csv` | 668 × 15 | Citas del canal digital: BDC, cliente, estatus, potencial de compra | Desempeño · BDC · ANOVA · Logística PDM |
| `Leads_Reales_Limpia.csv` | 28 × 15 | Leads reales por mes (28 meses): total, ilocalizable, etc. | Panorama · Embudo |
| `MKT_DIGITAL.csv` | 175 × 56 | Marketing digital por canal (inversión y resultados) | Desempeño · Marketing · ANOVA |
| `Plazas.csv` | 303 × 16 | Leads de plaza: fecha origen, producto, asesor, origen | Desempeño · Leads de plaza · ANOVA |
| `base_leads_limpia.csv` | 208 × 12 | Base de leads depurada: fecha de alta, mes, producto | Embudo · Modelos |
| `base_resumen_limpio.csv` | 30 × 26 | Resumen mensual integrado (30 meses): leads, efectivos, ventas, objetivo | Panorama · Regresiones |
| `bcs_modelos.csv` | 6 × 3 | Objetivo vs ventas reales por modelo BCS | Desempeño · Productos |
| `funnel_mensual.csv` | 18 × 11 | Embudo mensual por etapas (18 meses): leads → ventas | Embudo · Reg. del embudo |

## 4. Documentos entregables (`docs/`)

| Documento | Descripción |
|---|---|
| `Reporte de solución — Empresa del reto GAC.docx` | Reporte de solución de la empresa del reto |
| `Propuesta_GAC_Analisis_Predictivo.pptx` | Propuesta de análisis predictivo |
| `GAC Motor — Propuesta final (identidad GAC).pptx` / `GAC_Propuesta_Final.pdf` | Propuesta final (pptx editable + pdf) |
| `GAC — Diapositivas adicionales (embudo, modelo y gestión).pptx` | Diapositivas de apoyo |
| `Actividad 4 — Despliegue ANOVA (GAC).pptx` | Presentación del despliegue ANOVA (Etapa III) |
| `Proceso_de_Presentaciones_GAC.docx` | Proceso de presentaciones |
| `Regresion_GAC_en_ipynb.docx` | Documentación de la regresión |
| `GAC Dashboard Context.docx` | Contexto del dashboard |
| `Propuesta GAC.pdf` / `gac final.pdf` | Propuestas en pdf |

## 5. Cómo auditar

1. **Trazabilidad punta a punta:** cualquier cifra del dashboard → CSV depurado en `data/` → hoja cruda en `data/raw/` → transformación en el notebook de la etapa correspondiente.
2. **Reproducir el dashboard localmente:**
   ```bash
   pip install -r app/requirements.txt
   cd app && streamlit run app.py
   ```
   (Para correrlo tal cual, los CSV de `data/` deben estar junto a `app.py`, como en el repo de despliegue.)
3. **Modelos y ANOVA:** cada pestaña de la vista *Modelos Predictivos* muestra limpieza aplicada, hipótesis, estadísticos (F, p-valor, η², Levene) y hallazgo en lenguaje de negocio; los notebooks de etapa 2 y 3 son la evidencia de respaldo.
4. **Versión original por etapas:** `app/archivo/app_etapas_original.py` conserva la primera versión del análisis para comparar contra la versión final.

## 6. Notas y faltantes conocidos

- El **libro Excel original** (`Analisis GAC Full7agosto 2026.xlsx`) no está como archivo único; su contenido está en `data/raw/` como exportaciones CSV por hoja.
- El video `Actividad 4 — Despliegue ANOVA (GAC).mp4` no se incluye por tamaño; está la presentación pptx equivalente en `docs/`.
- Se conservó la versión más reciente de cada documento duplicado (`-2`, `(1)`).

---

*Proyecto académico — Minería de Datos, Tecnológico de Monterrey · Gabriel Omar Pérez Hernández (A01736195)*
