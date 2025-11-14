# Hospital Readmission Risk Analysis
Predicting Excess Readmission Risk Using CMS FY25 Hospital Readmissions Reduction Program Data

---

## Project Overview
Hospital readmission rates are a key indicator of healthcare quality. The CMS Hospital Readmissions Reduction Program (HRRP) penalizes hospitals whose readmission performance is worse than expected.

This project analyzes CMS FY25 HRRP data to understand:
- What factors influence hospital readmission performance
- Whether we can predict which hospitals exceed expected readmission ratios
- What insights healthcare administrators can use to improve outcomes

The project includes data cleaning, exploratory analysis, predictive modeling, and interpretation.

---

## Dataset
Source: Centers for Medicare & Medicaid Services (CMS)

File: FY_2025_Hospital_Readmissions_Reduction_Program_Hospital.csv  
Rows: 18,511  
Unique hospitals: 3,021  
States: 51  

Condition categories:
- READM-30-AMI-HRRP
- READM-30-CABG-HRRP
- READM-30-HF-HRRP
- READM-30-HIP-KNEE-HRRP
- READM-30-PN-HRRP
- READM-30-COPD-HRRP

A binary target variable was created:
- 1 = Excess Readmission Ratio greater than 1.0
- 0 = Equal to or better than expected

---

## 1. Data Cleaning
Cleaning steps included:
- Removing rows with missing key numeric fields
- Converting number strings such as "1,234" into integers
- Converting date fields into datetime format
- Standardizing categorical variables
- Saving a clean CSV file for EDA and modeling

---

## 2. Exploratory Data Analysis (EDA)

Distribution of Excess Readmission Ratios:  
Most hospitals cluster around a ratio of 1.0, meaning they perform close to CMS expectations. Higher ratios indicate worse-than-expected performance.

Predicted vs Expected Readmission Rates:  
A strong linear relationship indicates CMS's expected and predicted values are closely aligned.

Readmission Ratio by Condition:  
Medical conditions such as Heart Failure and COPD show consistent patterns, while surgical procedures such as Hip/Knee replacements show greater variability.

State-Level Performance:  
Some states show slightly higher average ratios, while others perform closer to or better than expected.

Geographic Map:  
A choropleth map highlights moderate regional differences in readmission performance across the country.

---

## 3. Feature Engineering
To avoid data leakage, only non-overlapping features were used in the model:
- State
- Measure Name
- Number of Discharges

Excluded features:
- Predicted Readmission Rate
- Expected Readmission Rate

Categorical variables were one-hot encoded.  
The data was split into train and test sets using a stratified split to maintain class balance.

---

## 4. Modeling

Two models were trained and evaluated.

Logistic Regression:
- ROC-AUC: approximately 0.63
- Performs moderately well
- Better at identifying hospitals with high readmission risk

Random Forest Classifier:
- ROC-AUC: approximately 0.61
- Captures non-linear relationships
- Provides feature importance rankings

The limited predictive power is expected due to the lack of patient-level clinical and demographic data.

---

## 5. Feature Importance (Random Forest)

Top contributing features:
- Number of Discharges (most influential)
- Condition types such as Heart Failure, COPD, Pneumonia, CABG, Hip/Knee
- State indicators such as FL, TX, CA, NY

This shows that hospital volume and condition type have a meaningful impact on readmission risk, while geographic factors contribute to a lesser extent.

---

## 6. Interpretation and Insights
Predicting excess readmission using only administrative hospital-level features is challenging. ROC-AUC scores around 0.61 to 0.63 are realistic given the limited dataset.

The models still captured useful patterns. Hospitals with higher volume and certain condition categories are more likely to show higher-than-expected readmissions. Some state-level differences were also observed.

More complete predictive modeling would require patient-level data, comorbidity scores, severity indices, and socioeconomic measures.


---

## 7. Conclusion
This project provides an end-to-end analysis of real CMS hospital readmission data. After performing data cleaning, EDA, modeling, and interpretation, the results show that administrative features alone offer limited predictive power. However, the project demonstrates clear patterns related to clinical condition type, hospital volume, and geographic factors.

The project establishes a strong foundation for healthcare analytics and highlights the need for richer datasets to build stronger predictive models.

---
