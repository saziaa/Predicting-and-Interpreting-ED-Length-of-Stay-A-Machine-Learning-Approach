# Predicting and Interpreting Emergency Department Length of Stay Using Machine Learning

## 📌 Project Overview

This project analyzes emergency department (ED) utilization and length of stay (LOS) across Canada using NACRS data (2003–2022). It provides actionable insights into which patient and visit factors influence LOS, helping hospitals optimize resource allocation and patient flow. Machine learning models, including Random Forest and CatBoost, were used to predict LOS, while SHAP values interpret feature contributions. Complementary survival analysis with a Cox proportional hazards model identifies statistically significant predictors of time-to-discharge.

## 🎯 Objectives

- Examine trends in ED visits across age, sex, and main presenting problems.
- Identify factors influencing ED length of stay.
- Predict LOS using machine learning and interpret key drivers.
- Complement predictive insights with statistical inference using survival analysis.

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

### 1. ED Visits by Age and Sex
- Males dominate younger age groups (0–14 years), while females outnumber males after 75 years.  
- **Why it matters:** Understanding demographic patterns helps hospitals anticipate demand across age and sex groups.

### 2. Overall ED Visit Trends
- Visits increased gradually from ~9.8M (2003) to 22.9M (2017).  
- Sharp rise in 2018–2019 due to inclusion of Quebec data.  
- Visits dropped to ~23.2M in 2020 (COVID-19 impact) and partially rebounded to ~28M in 2021.  
- **Why it matters:** Highlights temporal trends and the impact of reporting changes and external events on ED utilization.

### 3. Acuity Analysis
- Urgent cases had the highest volume (~90M), Resuscitation the lowest.  
- Median LOS: Emergent and Urgent > 280 minutes; Non-Urgent ~120 minutes.  
- **Why it matters:** High-acuity cases, though fewer, consume significantly more ED resources, guiding staffing and resource allocation.

### 4. Visit Disposition Analysis
- Admitted patients: longest median LOS (~380 min).  
- Transferred patients: median LOS ~220 min.  
- Deaths: shortest LOS (~125 min).  
- Most visits result in discharge home (~380M visits).  
- **Why it matters:** Disposition patterns strongly influence resource use; planning should consider both volume and LOS by disposition type.

### 5. Frequency of ED Problems
- Trauma: most visits (~70M) but short LOS (~130 min).  
- Unintentional falls: ~20M visits, LOS ~140 min.  
- Acute Myocardial Infarction: lower volume but long LOS (~280 min).  
- **Why it matters:** High-frequency conditions are less resource-intensive per visit; severe but less frequent problems require more ED resources per patient.

### 6. Triage Level × Visit Disposition and LOS
- Urgent and Emergent admissions: longest median LOS (528 and 496.5 min).  
- Less Urgent admissions: ~396 min; Non-Urgent and Resuscitation admissions: ~300 min.  
- Other dispositions: Urgent deaths ~289.5 min; Urgent transfers ~257 min.  
- **Why it matters:** Both triage acuity and disposition strongly drive LOS, emphasizing the need to manage high-acuity admissions efficiently.

## 🧩 Methodology
- **EDA:** Age, sex, triage, disposition, and main problem trends analyzed with descriptive statistics and visualizations to understand ED utilization patterns.
- **Machine Learning:** Linear Regression, Random Forest, and CatBoost used to predict LOS; SHAP applied for interpretability to identify key operational drivers.
- **Survival Analysis:** Cox Proportional Hazards model fitted to identify independent predictors of LOS and provide statistical inference on time-to-discharge.

## 🔑 Key Findings

**Q1: Age- and Sex-Stratified ED Utilization**
- The 20–44 age group had the highest ED visits: Males ~1.3M, Females ~0.9M.
- In adults 65+, females visited more (~0.7M) than males (~0.5M).
- Trauma was the most common problem, especially in males 20–44 (~6.8M) and females (~4.2M).
- Unintentional falls were most frequent in females 65+.
- Acute myocardial infarction affected primarily males 45+ and females 65+.
- Pneumonia visits were concentrated in 0–19 and 65+ age groups.
- Motor vehicle collisions peaked in males 20–44.

**Q2: Triage Level and LOS Patterns by Age and Sex**
- Median LOS increases with age and acuity:
    - Females 65+: Emergent = 384 min, Resuscitation = 348 min
    - Males 65+: Emergent = 384 min, Resuscitation = 285 min
- Younger patients (0–44) had shorter LOS even in high-acuity cases.
- Older adults consistently experienced the longest stays, particularly for emergent presentations.

**Q3: Visit Disposition Insights by Age/Sex**
- Discharges home were most frequent in the 20–44 age group for both sexes.
- Admissions and transfers were most common among 65+, reflecting higher acuity.
- Not seen / left without being seen occurred mainly in 20–44 age group.
- Disposition patterns are strongly age-dependent: older adults required more intensive care, younger adults more likely discharged.

**Q4: Predicting Length of Stay (LOS)**

**Modeling Performance:**
- Linear Regression: Test R² = 0.51, MAE ≈ 69 min
- Random Forest: Test R² = 0.685, MAE ≈ 43 min (best)
- CatBoost: Test R² = 0.679, MAE ≈ 47 min
- **Interpretation:** Non-linear models (RF, CatBoost) captured complex relationships better than linear regression.

**SHAP Analysis (Random Forest):**
- Key predictors: visit disposition and triage level.
- Discharged home / left without being seen → shorter LOS.
- Transfers / high-acuity triage → longer LOS.
- Certain conditions (pneumonia, motor vehicle collisions) had modest effects.

**Survival Analysis (CoxPH):**
- Sex was the only independent predictor (males slightly shorter LOS, HR = 1.12, p < 0.005).
- Main problems had minimal independent effect (HR ≈ 1).
- Age and fiscal year trends exist but required stratification due to proportional hazards assumption violations.

**Integrated Insight:**
- Survival analysis identifies statistically significant independent predictors (sex).
- SHAP identifies operational drivers (disposition, triage) that explain most variation in LOS.
- Combined, these methods provide a comprehensive understanding: both demographic and operational factors shape ED LOS, while clinical presentation alone is less predictive once disposition and acuity are considered.

🛠️ Tools & Technologies

- Programming Language: Python 3.x

- Data Manipulation & Analysis: Pandas, NumPy

- Visualization: Matplotlib, Seaborn, Plotly

- Machine Learning & Modeling: Scikit-learn, CatBoost

- Model Interpretability: SHAP

- Survival Analysis: Lifelines (Cox Proportional Hazards)

- Development Environment: Jupyter Notebook

- Version Control & Repository: Git & GitHub

## 📚 Reference
Canadian Institute for Health Information. NACRS emergency department visits and lengths of stay. Accessed October 2, 2025. Link
