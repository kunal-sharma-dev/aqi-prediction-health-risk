# AQI Prediction & Health Risk Analysis

An end-to-end data analysis and machine learning pipeline that fetches real-time air quality data,
predicts Air Quality Index (AQI), and classifies health risk levels using statistical testing and ML models.

## 📊 Data Source
This project fetches **real air quality data** using the **Open-Meteo Air Quality API**:
- Completely free — no API key or signup required
- Covers 6 major Indian cities: Delhi, Mumbai, Bangalore, Kolkata, Chennai, Hyderabad
- Fetches last 90 days of hourly data for PM2.5, PM10, NO2, SO2, CO, O3
- Automatically resampled to daily averages for analysis

> **Fallback:** If the API is unreachable, the pipeline automatically generates a realistic
> synthetic dataset with the same statistical structure so the full pipeline still runs end-to-end.

## 🔧 Pipeline Overview

**1. Data Collection**
- Real-time fetch from Open-Meteo Air Quality API (lat/lon based, no auth needed)
- AQI computed from PM2.5 using the standard US EPA formula
- Graceful fallback to synthetic data if API is unavailable

**2. Data Wrangling**
- Missing value handling (backward/forward fill + mean imputation)
- Outlier removal using IQR method
- Feature engineering: lag features (1/3/7 day), rolling averages, seasonal/date features
- Min-Max normalization, label encoding
- Dimensionality reduction with PCA

**3. Exploratory Data Analysis**
- Distribution plots, boxplots, scatter plots
- Correlation heatmaps
- Time-series AQI trends
- Seasonal pollution pattern analysis

**4. Statistical Testing**
- Independent t-test (AQI across cities)
- Chi-Square test (AQI category vs. season)
- One-way ANOVA (AQI variation across cities)
- Pearson & Spearman correlation (PM2.5 vs AQI)

**5. Machine Learning**
- **Random Forest Regressor** — predicts numeric AQI value
- **Random Forest Classifier** — classifies health risk (Good/Moderate/Poor/Severe)
- **K-Means Clustering** — identifies unsupervised pollution pattern groups

## 📈 Results
| Metric | Value |
|---|---|
| Regression RMSE | 10.62 |
| Regression R² | 0.966 |
| Classification Accuracy | 89.6% |
| Pearson r (PM2.5 vs AQI) | ~0.98 |

> Results shown on synthetic dataset. Real API results will vary based on live pollution levels.

## 🩺 Health Risk Advisory System
The model outputs a predicted AQI and maps it to a health advisory:
- ✅ **Good (0–50)** — Air quality is satisfactory. Enjoy outdoor activities.
- ⚠️ **Moderate (51–100)** — Sensitive groups should limit prolonged outdoor exertion.
- 🟠 **Poor (101–200)** — Everyone may experience effects. Reduce outdoor activity. Wear a mask.
- 🔴 **Severe (200+)** — Health alert. Avoid outdoors. Stay indoors. Use air purifiers.

## 🛠️ Tech Stack
Python, Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn, SciPy, Requests, Open-Meteo API

## 🚀 How to Run

**Option 1 — Google Colab (recommended, no setup needed):**
- Upload the `.ipynb` file to [colab.research.google.com](https://colab.research.google.com)
- Run all cells — data fetches automatically from the API

**Option 2 — Local Jupyter:**
```bash
pip install -r requirements.txt
jupyter notebook AQI_Prediction_Health_Risk.ipynb
```

## 📁 Files
| File | Description |
|---|---|
| `AQI_Prediction_Health_Risk.ipynb` | Main notebook — full pipeline |
| `requirements.txt` | Python dependencies |
| `README.md` | Project documentation |
