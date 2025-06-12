# Telecom Customer Churn Analysis

## Project Overview
This project analyzes customer churn patterns in a telecom dataset to identify key factors influencing customer attrition and develop predictive models to help inform retention strategies.

## Table of Contents
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Key Findings](#key-findings)
- [Model Performance](#model-performance)


## Project Structure
```
churn/
│
├── complete_churn_analysis.ipynb   # Main analysis notebook
├── telecom_churn.csv               # Dataset
├── requirements.txt                # Dependencies
├── final_report.md                 # Detailed findings report
└── README.md                       # This file
```

## Installation
To set up the project environment:

```bash
# Clone the repository
git clone <https://github.com/kristicoka/telecom_churn.gitl>
cd churn

# Create and activate a virtual environment (optional)
python -m venv churn_env
source churn_env/bin/activate  # On Windows: churn_env\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

## Dataset
The dataset (`telecom_churn.csv`) contains customer information from telecom providers with the following features:
- Customer demographics (age, gender, location)
- Service usage metrics (calls made, SMS sent, data used)
- Registration information
- Salary estimates
- Churn status (target variable)

The dataset consists of 243,553 records with 14 columns and an overall churn rate of 20.05%.

## Methodology

### Data Preprocessing
1. **Data Cleaning**
   - Handled negative usage values (affecting 2.3% of records)
   - Converted date strings to datetime objects
   - No missing values were found

2. **Feature Engineering**
   - Created time-based features from registration dates:
     - `tenure_days`
     - `registration_month`
     - `registration_quarter`
   - Derived usage metrics:
     - `calls_per_day`
     - `data_per_call`

3. **Data Transformation**
   - Encoded categorical variables using LabelEncoder
   - Standardized numerical features with StandardScaler
   - Addressed class imbalance using SMOTE (after train-test split)

### Model Development
Three machine learning models were developed and compared:
1. Random Forest Classifier
2. XGBoost Classifier
3. Logistic Regression (baseline)

Models were evaluated using:
- 5-fold cross-validation
- Classification metrics (precision, recall, F1-score)
- ROC curves and AUC
- Confusion matrices

## Key Findings

### Customer Behavior Insights
1. **Churn Distribution**
   - Overall churn rate: 20.05%
   - Significant variation across telecom partners (ranging from 19.99% to 20.36%)

2. **Temporal Patterns**
   - Higher churn rates in customers with shorter tenure (<6 months)
   - Peak registration months: March and December
   - Weekend registrations showed 15% higher retention rates

3. **Usage Patterns**
   - Weak correlation 


## Model Performance

### Cross-Validation Results
| Model | Mean CV Accuracy | Standard Deviation |
|-------|-----------------|-------------------|
| XGBoost | 0.8515 | ±0.3624 |
| Random Forest | 0.8442 | ±0.2761 |
| Logistic Regression | 0.5763 | ±0.0764 |

### Classification Reports

#### XGBoost
```
              precision    recall  f1-score   support

           0       0.80      1.00      0.89     38928
           1       0.29      0.00      0.00      9783

    accuracy                           0.80     48711
   macro avg       0.55      0.50      0.45     48711
weighted avg       0.70      0.80      0.71     48711
```

#### Random Forest
```
              precision    recall  f1-score   support

           0       0.80      0.95      0.87     38928
           1       0.20      0.05      0.08      9783

    accuracy                           0.77     48711
   macro avg       0.50      0.50      0.47     48711
weighted avg       0.68      0.77      0.71     48711
```

#### Logistic Regression
```
              precision    recall  f1-score   support

           0       0.80      0.58      0.68     38928
           1       0.20      0.42      0.28      9783

    accuracy                           0.55     48711
   macro avg       0.50      0.50      0.48     48711
weighted avg       0.68      0.55      0.59     48711
```

### Hyperparameter Tuning
Best parameters for Random Forest: `{'max_depth': 20, 'n_estimators': 200}`  
Best F1 score: 0.7363

### Model Comparison

| | Model | Mean CV Accuracy | CV Std Dev |
|---|-------------|-----------------|------------|
| 0 | Random Forest | 0.844174 | 0.138045 |
| 1 | XGBoost | 0.851543 | 0.181224 |
| 2 | Logistic Regression | 0.576317 | 0.038179 |
