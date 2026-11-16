# Olist: entregas tardías y satisfacción del cliente
### Proyecto final — Análisis de Datos, Inteligencia de Negocios y Aprendizaje Computacional (ITM)

**Equipo**

| Integrante | Rol | Entregable principal |
|---|---|---|
| Harol | ETL y calidad de datos | `src/etl.py`, `src/calidad.py`, `notebooks/01_etl.ipynb` |
| Leonel | Análisis exploratorio (EDA) y administración del repo | `notebooks/02_eda.ipynb` |
| Yulieth | Inteligencia de negocios y dashboard | `dashboard/` (Power BI), `notebooks/03_kpis_bi.ipynb` |
| Jalvi | Modelo predictivo | `src/features.py`, `notebooks/04_modelado.ipynb` |
| Todos | Conclusiones, informe, presentación y ética | `docs/` |

## Problema de negocio
Olist es un marketplace brasileño que conecta pequeños vendedores con clientes de todo el país. En los datos, **el 8 % de los
pedidos llega después de la fecha prometida**, y esos pedidos tienen **6 veces más probabilidad de recibir una reseña negativa**
(4,3 → 2,6 estrellas).

**Preguntas que responde el proyecto**
1. ¿Cómo se comportan las ventas, la logística y la satisfacción, y dónde están los problemas? *(EDA + dashboard)*
2. ¿Se puede anticipar, **en el momento de la compra**, qué pedidos llegarán tarde para actuar a tiempo? *(modelo predictivo)*

## Dataset
[Brazilian E-Commerce Public Dataset by Olist (Kaggle)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce):
unos 100 mil pedidos reales y anonimizados (2016–2018) en 9 tablas relacionadas. Además se usan **fuentes externas**: festivos
nacionales de Brasil, eventos comerciales y regiones del IBGE (en `src/config.py`).

## Estructura

```
├── data/
│   ├── raw/                 ← aquí van los 9 CSV de Kaggle (NO se suben a git)
│   └── processed/           ← lo genera el ETL: olist_dw.sqlite + dw/*.parquet|csv (NO se sube)
├── src/
│   ├── config.py            ← rutas, catálogos y fuentes externas
│   ├── etl.py               ← pipeline ETL automatizado (python -m src.etl)
│   ├── calidad.py           ← reglas de calidad de datos
│   └── features.py          ← variables del modelo (sin fuga de información)
├── notebooks/
│   ├── 01_etl.ipynb         ← recopilación, limpieza y transformación (ETL)
│   ├── 02_eda.ipynb         ← análisis exploratorio de datos
│   ├── 03_kpis_bi.ipynb     ← modelo de datos para BI y KPIs en SQL (cuadre del dashboard)
│   └── 04_modelado.ipynb    ← modelo predictivo de riesgo de retraso
├── dashboard/               ← .pbix, guía de construcción, medidas DAX, tema y capturas
├── docs/                    ← informe final, presentación y diccionario de datos
└── reports/figures/         ← gráficas exportadas por los notebooks
```

## Cómo ejecutarlo

```bash
# 1. Clonar e instalar dependencias (Python 3.10 o superior)
git clone https://github.com/Leoces95/aplicacion-negocios-analisis-datos-modelo-predictivo.git
cd aplicacion-negocios-analisis-datos-modelo-predictivo
python -m venv .venv
.venv\Scripts\activate            # Windows  (en Mac/Linux: source .venv/bin/activate)
pip install -r requirements.txt

# 2. Descargar el dataset de Kaggle y copiar los 9 CSV en data/raw/

# 3. Ejecutar el ETL (≈1 min): crea el data warehouse en data/processed/
python -m src.etl

# 4. Abrir los notebooks en orden: 01 → 02 → 03 → 04
jupyter lab
```

## Cómo trabajamos (resumen; el detalle está en [CONTRIBUTING.md](CONTRIBUTING.md))
- Nadie hace push directo a `main`: todo entra por **Pull Request** con al menos **1 aprobación**.
- Una rama por tarea: `feat/etl`, `feat/eda`, `feat/dashboard`, `feat/modelo`, `docs/informe`.
- Cada integrante es dueño de su notebook, para evitar conflictos de merge.
