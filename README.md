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

Q1: Age- and Sex-Stratified ED Utilization

Approach: Exploratory Data Analysis (EDA) of the Age & Sex and Main Problem tables.

Method: Population pyramids and cross-tabulations to identify utilization patterns across demographic groups.

Q2: Triage Level and LOS Patterns by Age and Sex

Approach: Stratified analysis using the Triage Level and Age & Sex tables.

Method: Compared median length of stay (LOS) across acuity categories and demographics to highlight workload and resource needs.

Q3: Visit Disposition Insights by Age/Sex

Approach: Analysis of the Visit Disposition table with demographic splits.

Method: Examined how discharge, admission, transfer, or death varied across groups and their impact on LOS.

Q4: Predicting Length of Stay (LOS)

Approach: Machine Learning + Survival Analysis.

Models Used: Linear Regression (LR), Random Forest (RF), and CatBoost.

Model Interpretation: Applied SHAP values to interpret feature importance and direction of effects.

Survival Analysis: Fitted a Cox Proportional Hazards (CoxPH) model to study time-to-discharge while accounting for censoring.
