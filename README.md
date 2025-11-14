Hospital Readmission Risk Analysis

Predicting Excess Readmission Risk Using CMS FY25 Hospital Readmissions Reduction Program Data

Project Overview

Hospital readmission rates are a key indicator of healthcare quality. The CMS Hospital Readmissions Reduction Program (HRRP) penalizes hospitals whose readmission performance is worse than expected.

This project analyzes real CMS FY25 HRRP data to understand:

What factors influence hospital readmission performance

Whether we can predict which hospitals exceed expected readmission ratios

What insights healthcare administrators can use to improve outcomes

The project includes data cleaning, exploratory analysis, predictive modeling, and interpretation.

Dataset

Source: Centers for Medicare & Medicaid Services (CMS)

Filename: FY_2025_Hospital_Readmissions_Reduction_Program_Hospital.csv
Rows: ~18,000
Unique hospitals: 3,021
States: 51

Condition (Measure) categories:

READM-30-AMI-HRRP

READM-30-CABG-HRRP

READM-30-HF-HRRP

READM-30-HIP-KNEE-HRRP

READM-30-PN-HRRP

READM-30-COPD-HRRP

A binary target column was created:

1 = Excess Readmission Ratio > 1.0

0 = Equal or better than expected

1. Data Cleaning

Cleaning steps included:

Removing rows missing important numeric fields

Converting number strings (for example “1,234”) into integers

Converting date fields into datetime format

Standardizing categorical variables

Saving a clean CSV file for analysis and modeling

2. Exploratory Data Analysis (EDA)

Distribution of Excess Readmission Ratios:
The ratio is centered near 1.0, meaning many hospitals perform close to CMS expectations. Hospitals above 1.0 perform worse than expected.

Predicted vs Expected Readmission Rates:
There is a strong linear relationship, showing alignment between CMS’s expected and predicted rates. Hospitals above the diagonal perform worse than expected.

Readmission Ratio by Condition:
Medical conditions such as heart failure and COPD show relatively consistent patterns. Surgical procedures such as hip/knee replacements show larger variation.

State-Level Performance:
Certain states (such as Massachusetts, New Jersey, and Illinois) show slightly higher average excess ratios. Some western states show lower ratios.

Geographic Map:
A choropleth map shows moderate regional differences, with some higher-risk clusters in the Northeast and South.

3. Feature Engineering

For modeling, only non-leaking features were used:

State

Measure Name

Number of Discharges

Excluded features (to avoid data leakage):

Predicted Readmission Rate

Expected Readmission Rate

Categorical variables were one-hot encoded.
Train/test split used stratification on the target variable.

4. Modeling

Two models were trained and evaluated.

Logistic Regression:

ROC-AUC: approximately 0.63

Performs moderately well

Stronger at identifying high-risk hospitals than low-risk ones

Random Forest Classifier:

ROC-AUC: approximately 0.61

Captures non-linear patterns

Provides feature importance values

Both models show limited predictive power because the dataset lacks patient-level details such as severity, comorbidities, and socioeconomic factors.

5. Feature Importance (Random Forest)

Top features included:

Number of Discharges (dominant predictor)

Condition categories such as Heart Failure, Pneumonia, COPD, CABG, Hip/Knee

Some state indicators such as FL, TX, CA, NY

This indicates:

Hospital volume plays a major role

Certain conditions are associated with higher readmission risk

Geographic differences exist but are less influential

6. Interpretation and Insights

Predicting excess readmission using only administrative hospital features is challenging. The limited AUC scores (0.61–0.63) are realistic given the lack of patient-level clinical data.

Even with limited features, the models identified meaningful patterns.
Hospitals with higher volume and certain condition types are more likely to exceed expected readmission levels. Geographic differences also contribute modestly.

The project shows that richer clinical data would be required to build a strong predictive model. However, administrative datasets like this still provide valuable insight into system-level patterns.

7. Project Structure
├── data/
│   ├── FY_2025_Hospital_Readmissions...csv
│   └── hospital_readmission_clean.csv
├── 01_data_cleaning.ipynb
├── 02_eda.ipynb
├── 03_modeling.ipynb
└── README.md

8. Conclusion

This project demonstrates an end-to-end analysis of real CMS hospital readmission data. After cleaning, exploring, and modeling the dataset, the results show that basic hospital-level operational features can provide limited but meaningful predictive insight into readmission performance.

The findings highlight the importance of richer data (patient demographics, comorbidities, socioeconomic indicators) for more accurate risk modeling. Nonetheless, this project offers a strong foundation for understanding hospital readmission patterns and forecasting high-risk hospitals using publicly available data.
