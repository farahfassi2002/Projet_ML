#  Historical Buildings Risk Assessment — Tunisia

A data science project for evaluating the degradation and structural risk of historical buildings across major Tunisian cities using geospatial data, climate indicators, and machine learning.

---

##  Overview

This project extracts, cleans, and models data on historical buildings (mosques, churches, museums, and other heritage sites) in **Tunis, Sfax, Kairouan, and Sousse**. It computes an **Infrastructure Risk Index (IRE)** based on physical and climatic features, then trains classification models to predict the risk category of each building.

---

##  Project Structure

```
├── dataCleaning1.ipynb        # Data extraction, cleaning, and exploration
├── Modelisation.ipynb         # Feature engineering, ML modeling, and visualization
├── data_brute_osm.csv         # Cleaned dataset exported from the data cleaning notebook
└── README.md
```

---

##  Pipeline

### 1. Data Collection & Cleaning (`dataCleaning1.ipynb`)

- Extracts geospatial data from **OpenStreetMap** using `osmnx` for 4 cities
- Targets buildings tagged as: `historic`, `mosque`, `church`, `synagogue`, `temple`, `museum`
- Filters for polygonal geometries and computes centroids (`lat`, `lon`)
- Calculates building surface area in m²
- Visualizes building type distributions and city-level counts
- Exports clean data to `data_brute_osm.csv`

### 2. Modeling (`Modelisation(1).ipynb`)

- Enriches the dataset with **city-level climate features**: humidity, annual rainfall, and thermal amplitude
- Computes a **composite climate score** and the **IRE (Infrastructure Risk Index)**
- Assigns one of four risk categories: `Stable`, `Modéré`, `Élevé`, `Critique`
- Simplifies to a binary classification: `Low_Risk` vs `High_Risk`
- Trains and evaluates three models:
  - Logistic Regression
  - Random Forest
  - XGBoost (with **Optuna** hyperparameter optimization)
- Selects the best model by F1-score and generates a **Folium interactive map** with color-coded risk markers

---

##  Cities Covered

| City      | Humidity | Annual Rainfall | Thermal Amplitude |
|-----------|----------|-----------------|-------------------|
| Tunis     | 68%      | 465 mm          | 14°C              |
| Sousse    | 65%      | 310 mm          | 15°C              |
| Sfax      | 58%      | 220 mm          | 18°C              |
| Kairouan  | 48%      | 280 mm          | 22°C              |

---

##  Installation

```bash
pip install osmnx geopandas folium scikit-learn xgboost shap optuna matplotlib seaborn pandas numpy
```

---

##  Usage

Run the notebooks in order:

```bash
jupyter notebook dataCleaning1.ipynb   # Step 1: Data extraction & cleaning
jupyter notebook Modelisation.ipynb    # Step 2: Modeling & risk mapping
```

`data_brute_osm.csv` must be present in the working directory before running the modeling notebook.

---

##  Models & Results

| Model                  | Metric    |
|------------------------|-----------|
| Logistic Regression    | Accuracy + F1  |
| Random Forest          | Accuracy + F1 |
| XGBoost + Optuna       | Accuracy + F1  |

The best-performing model is selected automatically and used to generate the final risk map.

---

##  Features Used

| Feature             | Description                                      |
|---------------------|--------------------------------------------------|
| `surface_m2`        | Building footprint area in square meters         |
| `lat` / `lon`       | Geographic coordinates of the centroid           |
| `humidite`          | City average humidity (%)                        |
| `pluie_annuelle`    | City average annual rainfall (mm)                |
| `amplitude_thermique` | City thermal amplitude (°C)                   |
| `score_climatique`  | Composite climate vulnerability score            |
| `IRE`               | Infrastructure Risk Index (target variable base) |

---

##  Output

The modeling notebook produces an interactive **Folium map** (`HTML`) with circle markers for each building, color-coded by risk level:

- 🟢 **Low Risk** — Stable or moderate degradation
- 🔴 **High Risk** — Elevated or critical degradation

Each marker displays the building name, city, IRE score, and risk category on hover.

---

##  Dependencies

- `osmnx` — OpenStreetMap data extraction
- `geopandas` — Geospatial data manipulation
- `folium` — Interactive map rendering
- `scikit-learn` — ML models and preprocessing
- `xgboost` — Gradient boosting classifier
- `optuna` — Hyperparameter optimization
- `matplotlib` / `seaborn` — Data visualization
- `pandas` / `numpy` — Data handling

---



This project is for academic and research purposes.
