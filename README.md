# Predictive Maintenance — Plastic Injection Molding Machine

Capstone project (B.Eng. Industrial Engineering, Kasetsart University)

A machine learning system for predicting equipment degradation in plastic injection molding
machines, enabling proactive maintenance before failure occurs.

---

## Overview

Industrial machines generate continuous sensor data that, when analyzed correctly, can reveal
early signs of wear or abnormal behavior. This project captures real-time thermal data from
a plastic injection molding machine via Modbus TCP, processes it, and applies regression
models to forecast equipment performance.

---

## System Architecture

**Data Collection** → **Preprocessing** → **Model Training & Evaluation** → **Alert (Line Notify)**

---

## Implementation

### 1. Data Collection (`readAx8.ipynb`)
- Connected to machine's thermal sensor over Modbus TCP (pyModbusTCP)
- Polled temperature registers continuously and decoded raw hex values into float readings
- Exported collected data as compressed CSV for downstream analysis

### 2. Predictive Model (`ML_Project_rev02.ipynb`)
- Preprocessed time-series thermal data: outlier removal via Z-score and IQR methods
- Evaluated multiple regression algorithms:
  - Linear Regression, Lasso, Ridge, Elastic Net
  - Polynomial Regression, KNN, Random Forest, Decision Tree, SVR, XGBoost
- Used K-Fold cross-validation and GridSearchCV for hyperparameter tuning
- Final model: **Lasso Regression** — best generalization performance, R² = 0.81
- Integrated Line Notify API to send proactive maintenance alerts

---

## Tech Stack

| Area | Tools |
|---|---|
| Language | Python |
| Data Collection | pyModbusTCP |
| Data Processing | pandas, NumPy |
| Machine Learning | scikit-learn, XGBoost |
| Visualization | matplotlib |
| Notification | Line Notify API |

---

## Results

- Achieved R² = 0.81 on test set
- Lasso regression outperformed 9 other candidate models in cross-validated evaluation
- System capable of forecasting temperature trends to trigger maintenance alerts proactively
