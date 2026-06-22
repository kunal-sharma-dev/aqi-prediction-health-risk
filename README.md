# AQI Prediction & Health Risk Analysis

An end-to-end data analysis and machine learning pipeline that predicts Air Quality Index (AQI) 
and classifies health risk levels using pollutant data, statistical testing, and ML models.

## 📊 Data Sources
This project is designed to fetch real-world air quality data from:
- **OpenAQ API** (`api.openaq.org`) — real-time pollutant measurements (PM2.5, PM10, NO2, SO2, CO, O3)
- **CPCB / data.gov.in** — historical city-day air quality data for Indian cities

> **Note:** Live API access can be unreliable (rate limits / endpoint changes). The pipeline 
> includes a fallback that generates a realistic synthetic dataset with the same statistical 
> structure as real pollutant data, so the full analysis and ML pipeline can still run end-to-end 
> for demonstration purposes.

## 🔧 Pipeline Overview

**1. Data Wrangling**
- Missing value handling (backward/forward fill + mean imputation)
- Outlier removal using IQR method
- Feature engineering: lag features, rolling averages, seasonal/date features
- Min-Max normalization, label encoding
- Dimensionality reduction with PCA

**2. Exploratory Data Analysis**
- Distribution plots, boxplots, scatter plots
- Correlation heatmaps
- Time-series AQI trends
- Seasonal pollution pattern analysis

**3. Statistical Testing**
- Independent t-test (AQI across cities)
- Chi-Square test (AQI category vs. season)
- One-way ANOVA (AQI variation across cities)
- Pearson & Spearman correlation (PM2.5 vs AQI)

**4. Machine Learning**
- **Random Forest Regressor** — predicts numeric AQI
- **Random Forest Classifier** — classifies health risk (Good/Moderate/Poor/Severe)
- **K-Means Clustering** — identifies unsupervised pollution pattern groups

## 📈 Results (on synthetic demonstration dataset)
| Metric | Value |
|---|---|
| Regression RMSE | 10.61 |
| Regression R² | 0.966 |
| Classification Accuracy | 89.1% |
| Pearson r (PM2.5 vs AQI) | 0.979 |

## 🩺 Health Risk Advisory System
The model outputs a predicted AQI and maps it to a health advisory:
- ✅ Good — safe for outdoor activity
- ⚠️ Moderate — sensitive groups should limit prolonged exposure
- 🟠 Poor — reduce outdoor activity, wear a mask
- 🔴 Severe — avoid outdoor activity, use air purifiers

## 🛠️ Tech Stack
Python, Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn, SciPy, Requests

## 🚀 How to Run
```bash
pip install -r requirements.txt
jupyter notebook AQI_Prediction_Health_Risk.ipynb
```
