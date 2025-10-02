# Predicting and Interpreting ED Length of Stay: A Machine Learning Approach

📌  **Project Overview**
This project analyzes emergency department (ED) utilization and length of stay (LOS) across Canada using national NACRS data from 2003–2022. It combines descriptive analyses, predictive modeling, and interpretability techniques to identify which patient and visit factors influence LOS. Machine learning models, including Random Forest and CatBoost, were used to predict LOS, with SHAP values applied to interpret feature contributions. In addition, a Cox proportional hazards (CoxPH) survival model was fitted to provide statistical inference on time-to-discharge, offering a complementary perspective to the machine learning findings.

🎯 **Objectives**
- To examine trends in ED utilization across age, sex, and presenting problems.

- To identify factors influencing ED length of stay.

- To predict LOS using machine learning models and interpret feature importance using SHAP.

- To complement predictive insights with statistical inference using survival analysis.

📊 **Data**

- Source:[CIHI – NACRS Emergency Department Visits and Lengths of Stay](https://www.cihi.ca/en/nacrs-emergency-department-visits-and-lengths-of-stay) 
- Coverage: Fiscal years 2003–2004 to 2021–2022, all provinces.
- Note: Quebec data included starting 2018–2019, which explains the sharp increase in reported visits.
- Dataset Structure (5 tables):
    - ED Visits – annual counts of ED visits, including high-acuity flags and overall length of stay.
    - Visit Disposition – outcomes of ED visits (e.g., discharged, admitted, transferred, death) with corresponding median LOS.
    - Triage Level – patient acuity levels (Resuscitation, Emergent, Urgent, Less Urgent, Non-Urgent) and associated LOS.
    - Main Problem – top presenting problems (e.g., trauma, pneumonia, acute myocardial infarction) with frequency and median LOS.
    - Age & Sex – visit counts and LOS distributions by age group and sex, useful for demographic analysis.
- Key Variables Used:

Age group

Sex

Triage level

Main presenting problem

Visit disposition

High-acuity flag

Median length of stay (LOS, minutes)
