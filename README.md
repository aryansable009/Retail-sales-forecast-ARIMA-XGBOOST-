# Retail Sales Forecasting: Hybrid ARIMA + XGBoost

This repository contains a short, rapid-turnaround forecasting project built in under **4 hours**, designed for a case scenario similar to FMCG forecasting (presented to Innocent Drinks during an interview). The aim was to predict weekly revenue for electronics sales (a proxy for high-value retail items) by blending classical time series analysis with machine learning.

---

## 📊 Project Overview

- **Data**: Synthetic daily retail transaction data including dates, product categories, quantities, and total revenue.
- **Focus**: Filtered on the *Electronics* category to capture meaningful volatility and simulate high-margin products.
- **Goal**: Forecast weekly revenue to aid in inventory & promotion planning.

---

## ⚙️ Approach

1. **Data Processing & Aggregation**
   - Converted daily transactions to **weekly revenue series** (52 data points across a year).

2. **Baseline Model: ARIMA(3,0,3)**
   - Confirmed data stationarity using the **ADF test (p < 0.00001)**.
   - Selected ARIMA order based on ACF & PACF plots.

3. **Residual Analysis**
   - Plotted ACF/PACF on ARIMA residuals, revealing remaining autocorrelation — a clear case for further modeling.

4. **Feature Engineering for XGBoost**
   - Created lag features (`lag_1`, `lag_2`, `lag_3`) and calendar features (`week_number`, `month`).

5. **Hybrid Modeling**
   - Trained XGBoost on residuals to learn patterns ARIMA missed.
   - Final prediction = **ARIMA forecast + XGBoost predicted residuals**.

6. **Validation**
   - Used **RMSE, MAE, MAPE, and R²** to compare ARIMA vs Hybrid.
   - Hybrid model consistently outperformed ARIMA-only.

---

## 🚀 Results

| Metric  | ARIMA  | Hybrid (ARIMA + XGBoost) | Improvement |
|---------|--------|--------------------------|-------------|
| RMSE    | 2412   | **2330**                 | ✅ Lower    |
| MAE     | 1707   | **1576**                 | ✅ Lower    |
| R²      | 0.23   | **0.27**                 | ✅ Better   |

---

## 🔍 Key Insights

- Even simple lag & calendar features combined with residual learning produced meaningful error reduction.
- Highlights the power of **hybrid models** in capturing both structured seasonality and irregular sales spikes common in retail.

---

## 🚀 Quick Start

```bash
git clone https://github.com/yourusername/retail-sales-forecasting-hybrid-arima-xgboost.git
cd retail-sales-forecasting-hybrid-arima-xgboost
pip install -r requirements.txt
jupyter notebook notebooks/Retails_forecast_inno1.ipynb
