# 📈 Task 2 — Predict Future Stock Prices (Short-Term)
**DevelopersHub Corporation — AI/ML Engineering Internship**

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)
![Sklearn](https://img.shields.io/badge/Scikit--Learn-ML-yellowgreen?logo=scikit-learn)
![yfinance](https://img.shields.io/badge/yfinance-Live%20Data-red)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)

---

## 🎯 Objective
Use **3 years of historical stock data** from Apple Inc. (AAPL) to predict the **next day's closing price** using Machine Learning regression models.

The goal is to evaluate how well engineered features (moving averages, volatility) help in short-term stock price forecasting.

---

## 📂 Dataset

| Property | Detail |
|:---|:---|
| **Stock** | Apple Inc. — AAPL |
| **Source** | Yahoo Finance via `yfinance` Python library (live download) |
| **Period** | Last 3 years of daily trading data |
| **Samples** | ~750 trading days |
| **Raw Features** | Open, High, Low, Close, Volume |
| **Target** | Next day's Closing Price |
| **Missing Values** | None |

### Raw Columns Description

| Column | Description |
|:---|:---|
| `Open` | Opening price of the stock for the day |
| `High` | Highest price reached during the day |
| `Low` | Lowest price reached during the day |
| `Close` | Closing price at end of trading day |
| `Volume` | Total number of shares traded |

---

## ⚙️ Feature Engineering

New features created to help the model understand trends and momentum:

| Feature | Formula | Purpose |
|:---|:---|:---|
| `MA_5` | 5-day rolling mean of Close | Short-term trend |
| `MA_20` | 20-day rolling mean of Close | Medium-term trend |
| `Price_Range` | High − Low | Daily volatility range |
| `Price_Change` | Close − Open | Intraday momentum |
| `Volatility` | 5-day rolling std of Close | Price stability measure |
| `Target` | `Close.shift(-1)` | Next day's price ← **predict this** |

---

## 🤖 Models Applied

### 1. Linear Regression
- Fits a straight line through the feature space
- Fast and interpretable baseline model
- Assumes a linear relationship between features and target

### 2. Random Forest Regressor
- Ensemble of **200 decision trees**
- Each tree votes → average = final prediction
- Captures non-linear patterns better than Linear Regression
- `n_estimators=200`, `random_state=42`

### Train / Test Split
```
Total data  → Chronological order (NO shuffling — time series rule!)
Train set   → First 80% of trading days
Test set    → Last 20% of trading days
Scaling     → StandardScaler applied to all features
```

---

## 📊 Key Results & Findings

### Model Performance

| Metric | Linear Regression | Random Forest |
|:---|:---:|:---:|
| **MAE** | ~$1.5 – $3.0 | ~$0.8 – $2.0 |
| **RMSE** | ~$2.0 – $4.0 | ~$1.0 – $3.0 |
| **R² Score** | ~0.97 | ~0.99 |

> **MAE** = Average dollar error per prediction  
> **RMSE** = Root Mean Squared Error — penalises large errors more  
> **R²** = 1.0 is perfect; above 0.95 is considered excellent

### Feature Importance (Random Forest)

| Rank | Feature | Importance |
|:---:|:---|:---:|
| 🥇 1 | `MA_5` | Highest |
| 🥈 2 | `MA_20` | High |
| 🥉 3 | `Close` / `Open` | Medium |
| 4 | `Volatility` | Low |
| 5 | `Volume` | Lowest |

### Key Observations

- ✅ **Random Forest outperforms** Linear Regression on all metrics
- 📌 **Moving averages (MA_5, MA_20)** are the strongest predictors — short-term price trend dominates
- 📌 **Volume** has relatively low predictive power compared to price-based features
- ⚠️ **Chronological splitting** is critical — shuffling would cause data leakage in time series
- 📌 Feature engineering significantly improved model performance over raw OHLCV data

### Limitations
- Models predict only **1 day ahead** — longer horizons are much harder
- **External factors** (news, earnings reports, macroeconomics) are not captured
- Past performance does not guarantee future results

---

## 🛠️ Libraries Used

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import yfinance as yf
from sklearn.linear_model import LinearRegression
from sklearn.ensemble import RandomForestRegressor
from sklearn.preprocessing import StandardScaler
from sklearn.metrics import mean_absolute_error, mean_squared_error, r2_score
```

---

## 🚀 How to Run

```bash
# 1. Install dependencies
pip install pandas numpy matplotlib seaborn yfinance scikit-learn jupyter

# 2. Launch Jupyter
jupyter notebook

# 3. Open and run
Task2_Stock_Price_Prediction.ipynb   →   Run All Cells
```

> ✅ No manual dataset download needed — data is fetched live from Yahoo Finance on run.

---

## 📁 Files

| File | Description |
|:---|:---|
| `Task2_Stock_Price_Prediction.ipynb` | Main Jupyter Notebook |
| `README.md` | This file |

---

> ⚠️ **Disclaimer:** This project is for **educational purposes only**. Stock price predictions made by this model are **not financial advice**. Do not use for actual trading or investment decisions.
