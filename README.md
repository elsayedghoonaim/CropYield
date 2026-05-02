# 🌾 Crop Yield Prediction

A machine learning project that predicts crop yield (hg/ha) for 101 countries using climate, pesticide, and historical FAO data. Includes a global multi-country analysis and a dedicated Egypt-focused notebook.

---

## 📁 Project Structure

```
CropYield/
├── yield_prediction.ipynb   # Global model — 101 countries, 10 crops
├── data.csv                 # Merged & cleaned dataset (global)
├── Data/
│   ├── yield.csv            # FAO crop yield data
│   ├── yield_df.csv         # Alternative FAO yield dataset
│   ├── temp.csv             # Average annual temperature by country
│   ├── rainfall.csv         # Average annual rainfall (mm/year)
│   └── pesticides.csv       # Pesticide use (tonnes of active ingredients)
└── Egypt/
    ├── yield_egypt.ipynb    # Egypt-specific analysis & model
    └── data.csv             # Egypt-filtered merged dataset
```

---

## 📊 Dataset

All data is sourced from publicly available datasets:

| Dataset | Source | Coverage |
|---|---|---|
| Crop Yield | [FAO](https://www.fao.org/faostat/) | 1961–2013 |
| Temperature | World / Berkeley Earth | 1849–2013 |
| Rainfall | World Bank | 1985–2013 |
| Pesticides | FAO | 1990–2013 |

**After merging and deduplication:** 25,938 rows × 7 columns, spanning **101 countries** and **10 crops** from **1990 to 2013**.

### Crops Covered
Maize, Potatoes, Rice (paddy), Wheat, Sorghum, Soybeans, Cassava, Yams, Sweet Potatoes, Plantains

### Features

| Feature | Description |
|---|---|
| `Area` | Country name |
| `Item` | Crop type |
| `Year` | Year (1990–2013) |
| `avg_temp` | Average annual temperature (°C) |
| `Pesticide_value` | Pesticide use (tonnes of active ingredients) |
| `avg_rain` | Average annual rainfall (mm/year) |
| `Yield_value` | **Target** — Crop yield (hg/ha) |

---

## 🧹 Data Preprocessing

- Merged 5 separate CSV files on `Area` and `Year`
- Removed 2,310 duplicate rows
- Converted `avg_rain` column from string (`".."`) to numeric, replacing invalid entries with `NaN`
- Filled 6 remaining nulls using forward fill (`ffill`)
- Applied `LabelEncoder` on categorical columns (`Area`, `Item`)
- Applied `StandardScaler` on numeric features

---

## 🤖 Models

Two models are trained and evaluated:

| Model | Description |
|---|---|
| `RandomForestRegressor` | Ensemble of decision trees, robust to outliers |
| `XGBRegressor` | Gradient boosting, optimized for speed and accuracy |

**Train/Test Split:** 80% / 20%

**Evaluation Metrics:** R² Score, MAE, MSE

---

## 🚀 Getting Started

### Requirements

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost
```

### Run

```bash
jupyter notebook yield_prediction.ipynb
```

For the Egypt-specific analysis:

```bash
jupyter notebook Egypt/yield_egypt.ipynb
```

---

## 🗺️ Egypt Analysis

The `Egypt/` subfolder contains a dedicated notebook that filters the global dataset to Egypt only, allowing for a more focused regional study of crop yield trends, climate correlation, and model performance specific to Egyptian agriculture.

---

## 📄 License

This project uses publicly available FAO and World Bank data. Free to use for research and educational purposes.
