# 🌫️ AQI Prediction — Indian Cities

A machine learning and data analytics project to analyze and predict the **Air Quality Index (AQI)** across Indian cities using city-level daily pollutant readings. Built with Python and visualized with an interactive Power BI dashboard.

---

## 📊 Power BI Dashboard

An interactive 4-page dashboard exploring the dataset from every angle — all pages support cross-filtering by City, AQI Category, Month, and Year.

### Page 1 — Air Quality Overview
High-level AQI distribution, city pollution rankings, and the scale of severe air quality events across India.

![Air Quality Overview](screenshots/dashboard_page1.png)

**Key insights:**
- **Average AQI: 166.46** across 26 cities and 24,850 records (2015–2020)
- **35.5% Moderate** days | **33.1% Satisfactory** | **5.4% Severe** | **1,000 total severe days**
- **Ahmedabad** leads the pollution table (~425 avg AQI), ahead of Delhi (~280) and Patna (~250)
- Right-skewed AQI distribution with peak around 80–120 and a long tail past 400

---

### Page 2 — Seasonal & Temporal Trends
Monthly and seasonal AQI patterns, capturing the recurring winter pollution cycle from 2015 to 2020.

![Seasonal & Temporal Trends](screenshots/dashboard_page2.png)

**Key insights:**
- **Winter (avg 225)** and **Autumn (avg 220)** are the most polluted seasons; **Monsoon (avg 115)** is the cleanest
- AQI peaks sharply in **October–January** every year — driven by temperature inversions and crop stubble burning
- July–September consistently record the lowest monthly average AQI (~120–130)
- Daily AQI trend shows a slight overall improvement toward 2020

---

### Page 3 — Pollutant Relationships & Model Insights
Correlation analysis, PM2.5 vs AQI scatter, Random Forest feature importance, and Power BI Key Influencers.

![Pollutant Relationships & Model Insights](screenshots/dashboard_page3.png)

**Key insights:**
- **PM2.5 (0.66)** and **PM10 (0.80)** have the highest correlation with AQI
- Random Forest confirms **PM2.5** as the dominant predictor (importance score > 0.40)
- **NOx > 78.24** increases average AQI by **205.4 units** (Key Influencers)
- PM2.5 vs AQI scatter shows a clear positive trend up to ~300 µg/m³, with non-linear spread at extremes

---

### Page 4 — Model Performance & Evaluation
Side-by-side evaluation of Linear Regression vs Random Forest on the held-out test set.

![Model Performance & Evaluation](screenshots/dashboard_page4.png)

| Metric | Linear Regression | Random Forest |
|--------|:----------------:|:-------------:|
| R² Score | 0.81 | **0.91** |
| RMSE | 59.27 | **40.72** |
| MAE | 31.01 | **20.68** |

**Best Performing Model: Random Forest** — R² = 0.91 | RMSE = 40.72 | MAE = 20.68

Random Forest reduces RMSE by ~31% and MAE by ~33% vs Linear Regression by capturing non-linear pollutant interaction effects.

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| Language | Python 3.x |
| Data Processing | Pandas, NumPy |
| Machine Learning | Scikit-learn |
| Visualization | Matplotlib, Seaborn |
| BI Dashboard | Power BI |
| Big Data | Apache Spark (PySpark) |
| Notebook | Jupyter Notebook |

---

## 📁 Files

```
├── AQI.ipynb              # Main notebook (EDA + ML pipeline)
├── AQI_Report.docx        # Full project report
├── screenshots/
│   ├── dashboard_page1.png   # Air Quality Overview
│   ├── dashboard_page2.png   # Seasonal & Temporal Trends
│   ├── dashboard_page3.png   # Pollutant Relationships & Model Insights
│   └── dashboard_page4.png   # Model Performance & Evaluation
└── README.md
```

---

## 📂 Dataset

The AQI dataset contains the following files:

| File | Description |
|------|-------------|
| `city_day.csv` | Daily AQI data by city ✅ |
| `city_hour.csv` | Hourly AQI data by city (62MB — not uploaded) |
| `station_day.csv` | Daily AQI data by station |
| `station_hour.csv` | Hourly AQI data by station (209MB — not uploaded) |
| `stations.csv` | Station metadata |

> **Note:** Due to GitHub's file size limit, `city_hour.csv` (62MB) and `station_hour.csv` (209MB) are not uploaded. Download the complete dataset from Kaggle: [Air Quality Data in India](https://www.kaggle.com/datasets/rohanrao/air-quality-data-in-india)

---

## 🔬 ML Pipeline Summary

1. **Data Loading** — `city_day.csv` with city-wise daily pollutant readings
2. **Null Handling** — Drop rows with null AQI; fill pollutant gaps with column-wise median
3. **Feature Engineering** — Extract `Month` and `Year` from Date for seasonality
4. **Feature Selection** — Drop `AQI_Bucket` (leakage), `City`, `Date` (identifiers)
5. **Train/Test Split** — Random 80/20 (appropriate for city-aggregated, non-time-series data)
6. **Linear Regression** — Baseline model; performs well due to AQI's formula-derived structure
7. **Random Forest** — 100 trees; captures non-linear pollutant interactions
8. **Evaluation** — R², RMSE, MAE, Actual vs Predicted, Residual plots

---

## 💡 Key Findings

- **North India dominates** pollution rankings — Ahmedabad, Delhi, Patna lead consistently
- **PM2.5 is the primary AQI driver** — confirmed by correlation matrix, Power BI Key Influencers, and RF feature importance
- **Seasonal pattern is strong** — Winter and Autumn are ~2× worse than Monsoon
- **Random 80/20 split is valid here** — city-aggregated data ≠ time-series; no temporal leakage risk
- **Linear Regression is a strong baseline** — AQI's mathematical formula makes the LR relationship inherently more linear than typical targets

---

## 🚀 Future Work

- City-level time-series forecasting with **ARIMA** or **Facebook Prophet**
- Incorporate **meteorological features** (wind speed, temperature, humidity)
- **Separate models per city** to capture location-specific dynamics
- Experiment with **XGBoost / LightGBM** for further gains
- Real-time AQI prediction pipeline connected to live **CPCB sensor data**

---

*Prepared by Ayeshkant Ray | SparkIIT Data Science | April 2026*
