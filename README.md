# GAC · Auditoría del Proceso Analítico

Repositorio de auditoría del proyecto de analítica comercial de **GAC Motor — Plaza Angelópolis**.
Agrupa en un solo lugar, organizado por etapa, todos los insumos y productos del proceso: datos limpios, notebook de trabajo, código del dashboard y documentación del pipeline.

**Dashboard desplegado (producto final):** https://dashboard-gac-53x7ncfkmh6t2yk75k7cmf.streamlit.app
**Repo de despliegue del dashboard:** https://github.com/a01736195-bot/Dashboard-GAC

> Este repo es para **auditar el proceso**; el repo de despliegue es el que mantiene la app en vivo.

---

## 1. Mapa del proceso

```
Fuente cruda (Excel de la plaza)
        │
        ▼
ETAPA I · Limpieza e integración ────────────────► data/  (CSVs depurados)
        │
        ▼
ETAPA II · Modelado predictivo ──────────────────► app/vistas_modelos.py
  · Correlaciones                                    (secciones por pestaña)
  · Regresión lineal simple y múltiple
  · Regresión del embudo
  · Regresión logística (PDM y Ventas)
        │
        ▼
ETAPA III · ANOVA ───────────────────────────────► app/vistas_modelos.py
  · Citas Digital por agente BDC                     (pestaña ANOVA)
  · Marketing por canal
  · Plazas
        │
        ▼
PRODUCTO · Dashboard Streamlit ──────────────────► app/app.py + app/vistas_modelos.py
  5 vistas: Panorama, Embudo, Desempeño,
  Modelos Predictivos y Laboratorio
```

## 2. Estructura del repositorio

| Carpeta | Contenido |
|---|---|
| `data/` | Los 9 CSV depurados que alimentan el dashboard y los modelos |
| `notebooks/` | `DASHBOARD_GAC.ipynb` — análisis univariado + regresión (despliegue) |
| `app/` | Código completo del dashboard: `app.py`, `vistas_modelos.py`, tema, requirements y versión original por etapas (`archivo/`) |

## 3. Diccionario de datos (`data/`)

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

## 4. Cómo auditar

1. **Trazabilidad de cifras:** cualquier número del dashboard se puede rastrear a un CSV de `data/`; el sidebar de la app muestra el conteo de registros de cada fuente.
2. **Reproducir el dashboard localmente:**
   ```bash
   pip install -r app/requirements.txt
   cd app && streamlit run app.py
   ```
   (Para correrlo tal cual, los CSV de `data/` deben estar junto a `app.py`, como en el repo de despliegue.)
3. **Modelos y ANOVA:** cada pestaña de la vista *Modelos Predictivos* muestra limpieza aplicada, hipótesis, estadísticos (F, p-valor, η², Levene) y hallazgo en lenguaje de negocio.
4. **Versión original por etapas:** `app/archivo/app_etapas_original.py` conserva la primera versión del análisis para comparar contra la versión final.

## 5. Material pendiente de integrar

Los siguientes insumos existen pero aún no están en este repo (se generaron fuera de esta carpeta de trabajo):

- [ ] Archivos **Excel originales** (fuente cruda entregada por la plaza)
- [ ] Notebook de **Etapa I** — limpieza e integración
- [ ] Notebook de **Etapa II** — modelado predictivo
- [ ] Notebook de **Etapa III** — ANOVA

Para integrarlos basta con copiarlos a la carpeta del proyecto; se agregan a `data/raw/` y `notebooks/` respectivamente y se actualiza esta lista.

---

*Proyecto académico — Minería de Datos, Tecnológico de Monterrey · Gabriel Omar Pérez Hernández (A01736195)*
