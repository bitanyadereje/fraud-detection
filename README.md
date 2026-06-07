# Interim‑1 Report: Fraud Detection – Task 1

**Author:** Your Name  
**Date:** 7 June 2026  
**Repository:** [GitHub link]

## 1. Data Cleaning and Preprocessing

- **E‑commerce dataset:** No missing values, no duplicates. `signup_time` and `purchase_time` converted to datetime.
- **Credit card dataset:** No missing values. `Amount` and `Time` scaled using StandardScaler.

## 2. Exploratory Data Analysis

### E‑commerce
- Fraud proportion: **9.5%** (imbalanced but not extreme).
- Fraud rate higher for: Direct traffic (10%), Chrome browser (9.5%), early morning hours (9–10 AM).
- Purchase value: fraud median slightly higher than legitimate.

### Credit Card
- Fraud proportion: **0.172%** (highly imbalanced).
- PCA features (V1–V28) show no anomalies.

## 3. IP‑to‑Country Enrichment

- Converted IP addresses to integers and merged with IP range data using `merge_asof`.
- Top fraud‑prone countries: Turkmenistan (100%), Namibia (43.5%), Sri Lanka (41.9%).
- Country column added as a categorical feature.

## 4. Feature Engineering

Engineered the following features for e‑commerce:

| Feature | Description |
|---------|-------------|
| `time_since_signup` | Seconds between signup and purchase |
| `hour_of_day` | Hour of purchase (0–23) |
| `day_of_week` | Day of week (Monday=0) |
| `purchase_count_1h` | Number of purchases by same user in last hour |
| `users_per_device` | How many users share a device |
| `transactions_per_ip` | Number of transactions from same IP |

For credit card, only scaling was applied (features are already PCA‑transformed).

## 5. Class Imbalance Handling Strategy

- **Current state:** E‑commerce 9.5% fraud; credit card 0.17% fraud.
- **Planned method (Task 2):** Apply **SMOTE** (Synthetic Minority Over‑sampling) **only on the training set** after train/test split. SMOTE creates synthetic fraud examples to balance the training set to 50/50.
- **Justification:** SMOTE reduces overfitting compared to naive oversampling and improves recall without discarding data (unlike undersampling).
- **Note:** For Interim‑1, we have only documented the strategy; SMOTE will be implemented in Task 2.

## 6. Deliverables

- Cleaned and feature‑engineered data saved in `data/processed/`:
  - `X_train.csv`, `X_test.csv`, `y_train.csv`, `y_test.csv` (e‑commerce)
  - `credit_X_train.csv`, `credit_X_test.csv`, `credit_y_train.csv`, `credit_y_test.csv` (credit card)
- All code in `notebooks/eda-fraud-data.ipynb` and `notebooks/eda-creditcard.ipynb`.
- This report.

## 7. Next Steps (Task 2)

- Train baseline (Logistic Regression) and ensemble (XGBoost) models.
- Use SMOTE on training set.
- Evaluate using AUC‑PR, F1‑score, confusion matrix.