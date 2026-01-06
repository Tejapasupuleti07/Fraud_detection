# Fraud Detection Using Machine Learning

## Project Overview
This project demonstrates the development of a machine learning model to detect fraudulent transactions for a financial company. Using a dataset of **6.3 million+ transactions**, the goal is to proactively identify fraud and provide actionable insights for prevention.

---

## Dataset
- **Source:** Fraud_Detection_Sample_Dataset.csv
- **Size:** 6,362,620 rows, 10 columns  
- **Columns:**
  - `step` – Time step of the transaction
  - `type` – Transaction type (TRANSFER, CASH_OUT, PAYMENT, etc.)
  - `amount` – Transaction amount
  - `oldbalanceOrg` – Sender balance before transaction
  - `newbalanceOrig` – Sender balance after transaction
  - `oldbalanceDest` – Receiver balance before transaction
  - `newbalanceDest` – Receiver balance after transaction
  - `isFraud` – Target variable (1 = fraud, 0 = non-fraud)
  - `isFlaggedFraud` – Rule-based flagged fraud (dropped to prevent data leakage)

---

## Project Steps

### 1. Data Cleaning
- Checked for missing values – none were found.
- Removed `isFlaggedFraud` to avoid leakage.
- Checked for outliers in `amount` and applied log transformation where necessary.
- Checked multicollinearity among numeric variables.

### 2. Exploratory Data Analysis (EDA)
- Fraud mostly occurs in **TRANSFER** and **CASH_OUT** transactions.
- Fraudulent transactions often involve **large amounts** or **sudden balance changes**.

### 3. Feature Engineering
- Categorical variable `type` converted to numerical features using **one-hot encoding**.
- Selected features: `step`, `amount`, `oldbalanceOrg`, `newbalanceOrig`, `oldbalanceDest`, `newbalanceDest`, and encoded `type` columns.

### 4. Handling Imbalanced Data
- Used **SMOTE (Synthetic Minority Oversampling Technique)** to balance the dataset, as fraud cases were <1%.

### 5. Model Building
- **Logistic Regression**: Baseline interpretable model.
- **Random Forest / XGBoost**: Tested for higher accuracy.
- Train-test split: 80%-20% after balancing.

### 6. Model Evaluation
- Metrics: **Precision, Recall, F1-score, ROC-AUC**
- Logistic Regression ROC-AUC: ~0.96 (example)
- Random Forest / XGBoost showed improved performance in capturing fraud.

### 7. Key Fraud Predictors
- Transaction type (TRANSFER, CASH_OUT)
- Large transaction amounts
- Sudden drop in sender balance
- Abnormal balance behavior in receiver account

---

## Business Insights
1. Fraudsters prefer TRANSFER and CASH_OUT transactions.
2. Large transaction amounts with unusual balance patterns are strong indicators of fraud.
3. Real-time monitoring and anomaly detection are critical for fraud prevention.
4. Multi-factor authentication and transaction limits can reduce fraud risks.

---

## How to Run
1. Install required packages:
```bash
pip install pandas numpy scikit-learn imbalanced-learn seaborn matplotlib xgboost
