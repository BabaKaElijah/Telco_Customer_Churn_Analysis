# Telco_Customer_Churn_Analysis
## Overview
This project analyzes customer churn for a telecommunications company using machine learning.
The goal is to predict whether a customer will leave the company and identify the key factors that drive churn.
The analysis includes data preprocessing, exploratory analysis, model building, and performance evaluation using recall-focused optimization.

## Business Objective

Customer churn directly affects business revenue.  
Predicting churn early allows the company to take proactive steps to retain customers through targeted offers or improved services.

### Main Goals
- Build a predictive model to classify customers as **Churn** or **Non-Churn**.  
- Improve **Recall** to capture as many churners as possible.  
- Provide **actionable business insights** based on feature importance.

## Dataset Information

**Source:** [Telco Customer Churn Dataset (Kaggle)](https://www.kaggle.com/blastchar/telco-customer-churn)  

**File Used:** `WA_Fn-UseC_-Telco-Customer-Churn.csv`  
**Records:** 7,043 customers  
**Features:** 21 customer-related variables and 1 target (**Churn**)

### Key Columns

| Feature | Description |
|----------|--------------|
| customerID | Unique ID for each customer |
| gender | Male or Female |
| SeniorCitizen | 1 if customer is a senior citizen |
| Partner | Whether the customer has a partner |
| Dependents | Whether the customer has dependents |
| tenure | Number of months the customer has stayed |
| PhoneService | Whether the customer has phone service |
| InternetService | Type of internet service (DSL, Fiber optic, None) |
| Contract | Contract type (Month-to-month, One year, Two year) |
| PaymentMethod | Payment type (Electronic check, Bank transfer, etc.) |
| MonthlyCharges | Amount charged monthly |
| TotalCharges | Total amount charged |
| Churn | Target variable (Yes = churned, No = retained) |

## Tools and Libraries

**Language:** Python  
**Environment:** Jupyter Notebook  

**Libraries Used:**  
- pandas  
- numpy  
- matplotlib  
- seaborn  
- scikit-learn  
- imbalanced-learn (SMOTE)  
- reportlab (for PDF reporting)  


## Data Preprocessing Steps

- Converted **TotalCharges** to numeric and handled 11 missing values.  
- Replaced "No internet/phone service" with "No".  
- Encoded binary columns (**Yes/No**) as **1/0**.  
- One-hot encoded multi-category features.  
- Scaled numerical features using **StandardScaler**.  
- **Final dataset shape:** 7,043 rows × 24 columns  


## Exploratory Data Analysis (EDA)

### Insights
- **Churn rate:** 26.6%  
- Customers with **month-to-month contracts**, **high monthly charges**, and **short tenure** are most likely to churn.  
- Customers with **Fiber optic internet** or paying via **Electronic check** have higher churn.  
- **Long-term contracts** (One-year or Two-year) reduce churn.  

### Example Visuals
- Distribution of churn 
![Churn Distribution](churn_distribution.png)
- Number of features Distribution
![Num Feature Distribution](num_features_distribution.png)
- Category features vs Churn
![Category features vs Churn](cat_features_vs_churn.png)

## Model Building

Two baseline models were built and evaluated using a train-test split (70/30).

### Model 1: Logistic Regression

| Metric       | Value |
|--------------|-------|
| Accuracy     | 0.75  |
| Recall       | 0.80  |
| Precision    | 0.52  |
| F1-score     | 0.63  |
| ROC AUC      | 0.85  |

**Confusion Matrix**  
```
[[950 344]]
 [ 95 372]]
```

### Model 2: Random Forest

| Metric       | Value |
|--------------|-------|
| Accuracy     | 0.79  |
| Recall       | 0.48  |
| Precision    | 0.64  |
| F1-score     | 0.55  |
| ROC AUC      | 0.83  |

**Confusion Matrix** 
```
[[1167  127]]
 [ 244  223]]
```
---

## Improving Recall (SMOTE Oversampling)

Since recall is critical for detecting churners, **SMOTE (Synthetic Minority Oversampling Technique)** was used to balance the dataset.

### Random Forest after SMOTE

| Metric       | Value |
|--------------|-------|
| Recall       | 0.62  |
| Precision    | 0.56  |
| F1-score     | 0.59  |
| ROC AUC      | 0.82  |

**Training set size**  
- Before SMOTE: (5282, 23)  
- After SMOTE: (7760, 23)  

This significantly improved the model’s ability to identify churners.

## Feature Importance

The top predictors of churn are:  
- Month-to-month contract (**most important**)  
- Short tenure  
- High monthly charges  
- Electronic check payment  
- Lack of TechSupport, OnlineSecurity, or Streaming services  

These features strongly influence customer retention.

![Category features vs Churn](cat_features_vs_churn.png)

---

## Business Recommendations

### Target High-Risk Customers
- Customers with month-to-month contracts and short tenure should be prioritized.

### Retention Incentives
- Offer discounts, contract upgrades, or loyalty programs to high-risk customers.

### Encourage Auto-Payments
- Reduce churn by promoting bank transfer or automatic payment methods.

### Enhance Service Value
- Offer bundled services such as TechSupport or OnlineSecurity to increase perceived value.

---

## Key Takeaways
- **Best performing model:** Logistic Regression (ROC-AUC 0.85, Recall 0.80)  
- SMOTE improved recall for Random Forest from 0.48 to 0.62  
- **Primary churn drivers:** contract type, tenure, monthly charges, and payment method  
- Project demonstrates data preprocessing, model evaluation, recall optimization, and business insight extraction

---

## Files Included
- `Telco_Customer_Churn_Analysis.ipynb` – Full notebook  
- `WA_Fn-UseC_-Telco-Customer-Churn.csv` – Dataset  
- `Telco_Customer_Churn_Overview.pdf` – Summary report  
- `README.md` – Project overview

