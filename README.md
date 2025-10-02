# Predicting and Interpreting ED Length of Stay: A Machine Learning Approach

## 📌 Project Overview

This project analyzes emergency department (ED) utilization and length of stay (LOS) across Canada using national NACRS data from 2003–2022. It combines descriptive analyses, predictive modeling, and interpretability techniques to identify which patient and visit factors influence LOS. Machine learning models, including Random Forest and CatBoost, were used to predict LOS, with SHAP values applied to interpret feature contributions. In addition, a Cox proportional hazards (CoxPH) survival model was fitted to provide statistical inference on time-to-discharge, offering a complementary perspective to the machine learning findings.

## 🎯 Objectives
- To examine trends in ED utilization across age, sex, and presenting problems.

- To identify factors influencing ED length of stay.

- To predict LOS using machine learning models and interpret feature importance using SHAP.

- To complement predictive insights with statistical inference using survival analysis.

## 🛢️ Data

- Source: [CIHI – NACRS Emergency Department Visits and Lengths of Stay](https://www.cihi.ca/en/nacrs-emergency-department-visits-and-lengths-of-stay) 
- Coverage: Fiscal years 2003–2004 to 2021–2022, all provinces.
- Note: Quebec data included starting 2018–2019, which explains the sharp increase in reported visits.
- Dataset Structure (5 tables):
    - ED Visits – annual counts of ED visits, including high-acuity flags and overall length of stay.
    - Visit Disposition – outcomes of ED visits (e.g., discharged, admitted, transferred, death) with corresponding median LOS.
    - Triage Level – patient acuity levels (Resuscitation, Emergent, Urgent, Less Urgent, Non-Urgent) and associated LOS.
    - Main Problem – top presenting problems (e.g., trauma, pneumonia, acute myocardial infarction) with frequency and median LOS.
    - Age & Sex – visit counts and LOS distributions by age group and sex, useful for demographic analysis.
- Key Variables Used:
    - Age group
    - Sex
    - Triage level
    - Main presenting problem
    - Visit disposition
    - Median length of stay (LOS, minutes)

## 📊 Exploratory Data Analysis (EDA)

Key findings from descriptive analysis:

### 1. ED Visits by Age and Sex:

- Pyramid analysis shows males dominate younger age groups (0–14 years), while females outnumber males after 75 years.

### 2. Overall ED Visit Trends:

- From 2003 to 2017, visits gradually increased from ~9.8M to 22.9M.

- In 2018–2019, there was a substantial rise due to Quebec inclusion.

- Visits dropped to ~23.2M in 2020 (COVID-19 impact) and partially rebounded to ~28M in 2021.

### 3. Acuity Analysis:

- Urgent cases had the highest volume (~90M), Resuscitation the lowest.

- Median LOS: Emergent and Urgent > 280 minutes; Non-Urgent ~120 minutes.

- High-acuity cases demand more ED resources despite being less frequent.

### 4. Visit Disposition Analysis:

- Admitted patients: longest median LOS (~380 min)

- Transferred patients: median LOS ~220 min

- Deaths: shortest LOS (~125 min)

- Most visits result in discharge home (~380M visits).

- High-acuity dispositions correlate with longer LOS; low-acuity dispositions dominate volume.

### 5. Frequency of ED Problems:

- Trauma: most visits (~70M) but short LOS (~130 min)

- Unintentional falls: ~20M visits, LOS ~140 min

- Acute Myocardial Infarction: low visit volume but long LOS (~280 min)

- High-frequency conditions are less resource-intensive; severe conditions require more ED resources per patient.

### 6. Triage Level × Visit Disposition and LOS:

- Urgent and Emergent admissions: longest median LOS (528 and 496.5 min, respectively)

- Less Urgent admissions: ~396 min

- Non-Urgent and Resuscitation admissions: ~300 min

- Other dispositions: Urgent deaths ~289.5 min; Urgent transfers ~257 min

- Both triage acuity and disposition strongly influence LOS.

## 🧩 Methodology

The analysis was guided by four research questions:

### Q1: Age- and Sex-Stratified ED Utilization

- Approach: Exploratory Data Analysis (EDA) of the Age & Sex and Main Problem tables.

- Method: Population pyramids and cross-tabulations to identify utilization patterns across demographic groups.

### Q2: Triage Level and LOS Patterns by Age and Sex

- Approach: Stratified analysis using the Triage Level and Age & Sex tables.

- Method: Compared median length of stay (LOS) across acuity categories and demographics to highlight workload and resource needs.

### Q3: Visit Disposition Insights by Age/Sex

- Approach: Analysis of the Visit Disposition table with demographic splits.

- Method: Examined how discharge, admission, transfer, or death varied across groups and their impact on LOS.

### Q4: Predicting Length of Stay (LOS)

- Approach: Machine Learning + Survival Analysis.

    - Models Used: Linear Regression (LR), Random Forest (RF), and CatBoost.

    - Model Interpretation: Applied SHAP values to interpret feature importance and direction of effects.

    - Survival Analysis: Fitted a Cox Proportional Hazards (CoxPH) model to study time-to-discharge while accounting for censoring.

## 🔑 Key Findings

**Q1: Age- and Sex-Stratified ED Utilization**

- The 20–44 age group accounts for the highest ED visits:

    - Males: ~1.3 million visits

    - Females: ~0.9 million visits

- In older adults (65+), females visit more frequently (~0.7 million) than males (~0.5 million).

- Trauma is the most common presenting problem across all ages, especially in males aged 20–44 (~6.8 million) and females (~4.2 million).

- Unintentional falls are most frequent among females aged 65+.

- Acute myocardial infarction predominantly affects males 45+ and females 65+.

- Pneumonia visits are concentrated in 0–19 and 65+ age groups for both sexes.

- Motor vehicle collisions peak in males aged 20–44.

**Q2: Triage Level and LOS Patterns by Age and Sex**

- Median length of stay (LOS) increases with age and acuity:

    - Females 65+: Emergent = 384 min, Resuscitation = 348 min

    - Males 65+: Emergent = 384 min, Resuscitation = 285 min

- Younger patients (0–44) have shorter LOS even for high-acuity cases.

- Older adults consistently experience the longest stays, particularly for emergent presentations.

**Q3: Visit Disposition Insights by Age/Sex**

- Discharges home are most frequent in 20–44 age group for both sexes.

- Admissions and transfers are most common among 65+, reflecting higher comorbidity and acuity.

- Not seen / left without being seen occurs mainly in 20–44 age group.

- Disposition patterns are strongly age-dependent: older adults require more intensive care, younger adults are more likely discharged.

**Q4: Predicting Length of Stay (LOS)**

### Modeling Performance:

- Linear Regression: Test R² = 0.51, MAE ≈ 69 min

- Random Forest: Test R² = 0.685, MAE ≈ 43 min (best performance)

- CatBoost: Test R² = 0.679, MAE ≈ 47 min

- **Interpretation**: Non-linear models (RF, CatBoost) better capture complex relationships between triage, disposition, acuity, and main problem.

### SHAP Analysis (Random Forest):

- Most important predictors: visit disposition and triage level

- Patients discharged home or left without being seen have shorter LOS

- Transfers and high-acuity triage increase LOS

- Certain clinical problems (e.g., pneumonia, motor vehicle collisions) have modest effects

### Survival Analysis (CoxPH):

- Sex is the only independent predictor of LOS (males slightly shorter, HR = 1.12, p < 0.005)

- Main problems have minimal independent effect (HR ≈ 1)

- Age and fiscal year trends exist but require stratification due to proportional hazards assumption violations

### Integrated Insight:

- Survival analysis identifies statistically significant independent predictors (sex).

- SHAP interpretation identifies operational drivers (disposition, triage) that explain most variation in LOS.

- Together, these methods provide a comprehensive understanding: operational and demographic factors both shape ED length of stay, while clinical presentation alone is less predictive once disposition and acuity are considered.

 - SHAP interpretation identifies operational drivers (disposition, triage) that explain most variation in LOS.

Together, these methods provide a comprehensive understanding: operational and demographic factors both shape ED length of stay, while clinical presentation alone is less predictive once disposition and acuity are considered.

🛠️ Tools & Technologies

- Programming Language: Python 3.x

- Data Manipulation & Analysis: Pandas, NumPy

- Visualization: Matplotlib, Seaborn, Plotly

- Machine Learning & Modeling: Scikit-learn, CatBoost

- Model Interpretability: SHAP

- Survival Analysis: Lifelines (Cox Proportional Hazards)

- Development Environment: Jupyter Notebook

- Version Control & Repository: Git & GitHub

## 📁 Repository Organization
## 📚 Reference
Canadian Institute for Health Information. NACRS emergency department visits and lengths of stay. Accessed October 2, 2025. Link
