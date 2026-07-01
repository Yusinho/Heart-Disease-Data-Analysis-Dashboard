# ❤️ Heart Disease Data Analysis Dashboard

### A Power BI Cardiovascular Risk Intelligence Project | California Hospital Association (Simulated)

**By Yusuf Shotunde — Data Analyst**

---

## 📌 Table of Contents

1. [Project Overview](#-project-overview)
2. [Objective](#-objective)
3. [Dataset Description](#-dataset-description)
4. [Data Preparation & Feature Engineering](#-data-preparation--feature-engineering)
5. [Data Modeling in Power BI](#-data-modeling-in-power-bi)
6. [Dashboard Architecture](#-dashboard-architecture)
7. [Detailed Findings](#-detailed-findings)
8. [Independent Statistical Validation](#-independent-statistical-validation)
9. [Data Quality Notes](#-data-quality-notes)
10. [Key Insights](#-key-insights)
11. [Recommendations](#-recommendations)
12. [Tools & Tech Stack](#-tools--tech-stack)
13. [How to Use This Repo](#-how-to-use-this-repo)
14. [Author](#-author)
15. [Disclaimer](#-disclaimer)

---

## 🎯 Project Overview

This project transforms a **10,000-patient clinical dataset** into an interactive Power BI cardiovascular risk dashboard. It combines data cleaning and feature engineering in Power Query, DAX-driven KPI modeling, and demographic/clinical risk segmentation to give healthcare stakeholders a fast, visual read on heart disease prevalence and its associated risk factors.

The workbook and dashboard were also presented as a 16-slide investigative report (included in this repo), walking through the methodology, demographic analysis, modifiable risk factors (smoking, diabetes), and clinical indicators (triglycerides, CRP, blood pressure, BMI) that shape cardiovascular risk in this dataset.

---

## 🎯 Objective

The stated objective of the analysis, carried directly from the source presentation, was to:

> **Transform raw clinical data into actionable cardiovascular intelligence.**

Specifically, the project set out to:
- Identify demographic and clinical patterns associated with heart disease
- Evaluate behavioral and metabolic risk factors
- Measure overall disease prevalence
- Develop a decision-support dashboard for healthcare insight

---

## 🗂️ Dataset Description

The source dataset (`heart_disease.csv`) contains **10,000 patient records** across **21 fields**:

| Category | Fields |
|---|---|
| **Demographics** | Age, Gender |
| **Clinical Measurements** | Blood Pressure, Cholesterol Level, BMI, Triglyceride Level, Fasting Blood Sugar, CRP Level, Homocysteine Level |
| **Behavioral Factors** | Exercise Habits, Smoking, Alcohol Consumption, Stress Level, Sleep Hours, Sugar Consumption |
| **Medical History** | Family Heart Disease, Diabetes |
| **Derived Risk Flags** | High Blood Pressure, Low HDL Cholesterol, High LDL Cholesterol |
| **Target Variable** | Heart Disease Status (Yes/No) |

**Population-level summary (all 10,000 patients):**
- Average age: **49.3 years** (range 18–80)
- Gender split: **50.0% Male (5,003) / 49.8% Female (4,978)**
- Heart Disease prevalence: **2,000 of 10,000 patients (20.0%)**

---

## 🧹 Data Preparation & Feature Engineering

Data cleaning and transformation were performed in **Power Query**, with categorical groupings engineered from continuous clinical fields to enable clearer segmentation on the dashboard:

| Derived Field | Category Rule |
|---|---|
| **Age Group** | Young < 40 · Middle Aged 40–55 · Senior 56–70 · Elderly > 70 |
| **Cholesterol Category** | Normal < 200 · Borderline 200–239 · High ≥ 240 |
| **BMI Category** | Underweight < 18.5 · Normal 18.5–24.9 · Overweight 25–29.9 · Obese ≥ 30 |
| **CRP Category** | Low < 1.0 · Medium 1.0–3.0 · High > 3.0 |
| **Triglyceride Category** | Normal < 150 · Borderline 150–199 · High 200–399 · Very High ≥ 400 |
| **Blood Pressure Category** | Normal < 120 · Elevated 120–139 · High Stage 1: 140–159 · High Stage 2 ≥ 160 |
| **Risk Category** | Composite score across risk flags → Low / Medium / High Risk |

Data types were also standardized (e.g., Age and Heart Disease Status set as whole numbers; category fields set as text) to ensure clean aggregation behavior in downstream DAX measures.

---

## 📐 Data Modeling in Power BI

The dataset was structured as a **single fact table**, with all segmentation handled at the transformation stage rather than through separate dimension tables — a deliberate simplification given the dataset's flat, single-grain structure (one row per patient).

**DAX measures created:**
- Total Patients
- Total Heart Disease Cases
- Disease Rate %
- Average Age
- High Risk %

**Slicers:**
- Age Group
- Gender
- Diabetes
- Smoking
- Risk Category

This single-fact-table design was optimized for **real-time slicer interaction** without the overhead of a full star schema, appropriate for a dataset of this size and grain.

---

## 🏗️ Dashboard Architecture

The dashboard is a **single-page interactive canvas**, organized into four zones:

<img width="1428" height="803" alt="Heart Disease Data Analysis Dashboard" src="https://github.com/user-attachments/assets/ed032f4f-95d7-4d5c-a388-b8271d335d63" />

### Top Row — Headline KPIs
- **Total Patients:** 10,000
- **Heart Disease Cases:** 2,000
- **Heart Disease Rate:** 20%
- **Average Age:** 49.2 years
- **High Risk %:** 31.8%

### Demographic Panel
- **Heart Disease Cases by Age Group** — Young 699, Middle Aged 465, Senior 465, Elderly 357
- **Heart Disease Cases by Gender** — Female 51.46% (~1,030) / Male 48.54% (~969)

### Behavioral & Metabolic Risk Panel
- **Heart Disease Cases by Cholesterol Category** — High 824, Normal 648, Borderline 514
- **Heart Disease Cases by Smoking** — Yes 1,025, No 961
- **Heart Disease Cases by Diabetes** — No 1.01K, Yes 0.98K

### Clinical Indicators Panel
- **Triglyceride Distribution** — High 1,314, Borderline 351, Normal 315, Very High 6
- **CRP Distribution** — a high-to-low gradient view, with High CRP (~1.84K) far outweighing Low CRP (~0.15K)
- **Blood Pressure Category** — High Stage 1: 652, High Stage 2: 650, Elevated: 643, Normal: 41
- **Heart Disease Cases by BMI Category** — Obese 953, Normal 514, Overweight 468, Underweight 51

### Interactivity
- **Slicers:** Age Group, Gender, Smoking, Diabetes, Risk Category — enabling any combination filter (e.g., "female smokers in the Senior age group")

---

## 🔎 Detailed Findings

### Demographic Analysis
The Young cohort (under 40) represents the largest heart-disease-case group at 699 patients, with Middle Aged and Senior groups showing an identical count of 465 patients each, and Elderly the smallest at 357. Gender distribution among heart disease cases is close to even, with a slight female majority (51.46% vs. 48.54% male).

### Risk Factor Analysis — Cholesterol & Smoking
High cholesterol is the most prevalent category among heart disease cases (824 patients), ahead of Normal (648) and Borderline (514). Smoking is also common among heart disease cases, with 1,025 identified as smokers versus 961 non-smokers among the affected population — a roughly 52%/48% split.

### Risk Factor Analysis — Diabetes
Diabetes status among heart disease cases is close to an even split: 1,010 non-diabetic vs. 980 diabetic patients (49.2% prevalence within the affected group).

### Clinical Indicators — Triglycerides & CRP
The majority of heart disease cases fall into the High triglyceride category (1,314 patients) — more than double the combined Normal and Borderline counts. CRP (C-Reactive Protein, an inflammatory marker) shows a similarly skewed pattern, with roughly 1.84K high-CRP cases against just 0.15K low-CRP cases.

### Clinical Indicators — Blood Pressure & BMI
Elevated and Stage 1/Stage 2 hypertension categories dominate, collectively accounting for the vast majority of heart disease cases versus just 41 patients in the Normal blood pressure range. Obesity is the leading BMI category among heart disease cases (953 patients) — nearly double the Normal-weight count (514).

---

## 🧪 Independent Statistical Validation

To verify the dashboard and stress-test its conclusions, the raw `heart_disease.csv` file was independently re-analyzed in Python (pandas) for this report. Two things came out of that check — one confirms the dashboard, and one adds an important layer of analytical nuance.

### ✅ Category counts reconcile closely
Re-applying the exact Power Query category rules above to the raw data reproduced the dashboard's figures closely: e.g., High Cholesterol 821 (dashboard: 824), Obese 955 (dashboard: 953), High Triglyceride 1,325 (dashboard: 1,314), Elevated/Stage 1/Stage 2 Blood Pressure 687/656/653 (dashboard: 643/652/650). The small differences (under 2%) are consistent with normal rounding and filter-context differences between Power BI and a standalone pandas recomputation, and confirm the dashboard's category logic is sound.

### ⚠️ Prevalence rates tell a different story than raw counts
The dashboard's charts show the **count of heart disease cases within each category** — which naturally scales with how large that category is in the overall population. To check whether these risk factors are actually *associated* with higher heart disease risk (rather than just being large groups), this analysis computed the heart disease **rate** (%) within each subgroup, across the full 10,000-patient dataset:

| Risk Factor | Rate Among "Yes"/High-Risk Group | Rate Among "No"/Lower-Risk Group |
|---|---|---|
| Smoking | 20.1% | 19.9% |
| Diabetes | 19.9% | 20.1% |
| Family Heart Disease | 19.7% | 20.2% |
| High Blood Pressure (flag) | 20.1% | 19.9% |
| High LDL Cholesterol | 20.3% | 19.7% |
| Alcohol Consumption (High) | 21.0% | ~19.4–20.4% (Low/Medium) |
| Stress Level | 18.7–21.4% across Low/Medium/High |
| Gender | Female 20.7% / Male 19.4% |

Across every behavioral and clinical factor tested, the heart disease rate stayed within a narrow **18.7%–21.4%** band — statistically indistinguishable from the overall 20.0% base rate. Mean values of continuous clinical markers (Cholesterol, BMI, Triglycerides, CRP, Blood Pressure, Fasting Blood Sugar) were also nearly identical between patients with and without heart disease.

**What this means:** this specific dataset does not show the modifiable risk factors (smoking, diabetes, cholesterol, BMI, blood pressure, CRP) actually elevating heart disease *rate* — the large raw counts for "High," "Obese," or "Smoker" categories in the dashboard largely reflect how common those categories are across the *entire* patient population (disease and non-disease alike), not a concentration of risk within them. This is a common and important distinction in dashboard design: **a count-based chart answers "where is the disease burden?" (useful for resource planning), while a rate-based chart answers "what increases individual risk?" (useful for clinical targeting)** — and this dataset, in its current form, only clearly supports the former.

This nuance doesn't diminish the dashboard's value as an operational/demographic profiling tool — it simply means any clinical "X causes/predicts heart disease" claims drawn from the raw case-count charts should be validated with rate-based analysis (as done here) before being used to guide screening or treatment prioritization.

---

## 🧹 Data Quality Notes

- **Alcohol Consumption** has a notably high missing-value rate (**25.9%**, 2,586 of 10,000 records) — substantially higher than any other field (all others are under 0.3% missing). Any analysis involving this field should account for this gap; it may represent a genuine "None/Non-drinker" category collapsed into missing values rather than true data loss.
- All other fields have negligible missingness (0.19%–0.30%), consistent with light random data entry gaps rather than a systemic collection issue.
- The dataset's near-uniform age distribution (18–80) and the flat ~20% disease rate across every subgroup are consistent with a **synthetically generated or randomized practice dataset** rather than real-world clinical data with organic risk correlations — worth noting explicitly for anyone building on this analysis.

---

## 💡 Key Insights

1. **Overall prevalence is 20%** — 1 in 5 patients in this dataset carries a heart disease diagnosis, with 31.8% of the total population classified as High Risk under the composite risk scoring model.
2. **The patient population skews younger** among heart disease cases, with the Young (<40) age band contributing the largest single group — worth further investigation into whether this reflects early-onset risk or simply the underlying age distribution of the sampled population.
3. **Gender distribution is balanced**, with heart disease cases split close to evenly (51.46% female / 48.54% male), meaning findings are broadly applicable across gender lines.
4. **High-burden categories are High Cholesterol, High Triglycerides, High CRP, elevated Blood Pressure, and Obesity** — these represent the largest raw patient counts among heart disease cases and are useful for operational planning (e.g., where to allocate screening resources).
5. **Rate-based validation did not confirm a measurable risk gradient** for any single factor tested in this dataset — a finding that should inform how confidently this specific dataset is used to support causal or predictive claims (see [Independent Statistical Validation](#-independent-statistical-validation)).
6. **Data completeness is strong**, apart from the Alcohol Consumption field, which should be handled carefully in any downstream modeling.

---

## 🧭 Recommendations

1. **Use the dashboard's count-based views for operational planning** (e.g., screening resource allocation, clinic staffing for hypertension/obesity management) — this is where the dashboard is on strongest analytical ground.
2. **Pair any risk-factor claims with rate-based validation** before using them to guide clinical prioritization, screening protocols, or patient communication — as demonstrated in this report's independent validation section.
3. **Investigate the Alcohol Consumption missing-value pattern** to determine whether it represents a genuine "non-drinker" category before including it in further modeling.
4. **Validate findings against a real-world clinical dataset** before applying any of this project's conclusions in an actual healthcare decision-support context — this project is a strong demonstration of BI/DAX methodology, but its source data shows characteristics of a synthetic or randomized dataset.
5. **Extend the risk model** with a validated, published cardiovascular risk score (e.g., Framingham or ASCVD) if this dashboard is to be adapted for real clinical use, since the current composite Risk Category was purpose-built for this dataset and demonstration.

---

## 🛠️ Tools & Tech Stack

| Tool | Purpose |
|---|---|
| **Microsoft Power BI** | Dashboard build, DAX measures, slicer-driven interactivity |
| **Power Query** | Data cleaning, type standardization, and category feature engineering |
| **DAX** | Total Patients, Total Heart Disease Cases, Disease Rate %, Average Age, High Risk % measures |
| **Python (pandas)** | Independent validation and rate-based statistical cross-check for this report |
| **PowerPoint** | 16-slide investigative presentation accompanying the dashboard |

---

## 📂 How to Use This Repo

```
├── data/
│   └── heart_disease.csv
├── dashboard/
│   └── heart_disease_dashboard.pbix
├── report/
│   └── Yusuf_Shotunde-_Heart_Disease_Data_Analysis_Report.pptx
└── README.md
```

1. Clone or download this repository
2. Open `heart_disease_dashboard.pbix` in **Power BI Desktop** to explore the live dashboard
3. Use the **Age Group / Gender / Smoking / Diabetes / Risk Category** slicers to filter all visuals interactively
4. Review the accompanying `.pptx` for the full narrative walkthrough of methodology and findings
5. `heart_disease.csv` is included for independent analysis or reproduction of the validation checks in this README

---

## 👤 Author

**Yusuf Shotunde**
*Data Analyst*
*(LinkedIn- www.linkedin.com/in/yusuf-shotunde / GitHub- https://github.com/Yusinho)*

---

## 📄 Disclaimer

This project was built for **portfolio and educational demonstration purposes**, presented in the context of the California Hospital Association as a simulated client scenario. The underlying dataset shows characteristics consistent with synthetic/randomized data (a near-flat ~20% disease rate across all tested risk factors) rather than organically collected clinical data, as detailed in the Independent Statistical Validation section. No conclusions in this report should be used to inform real clinical, diagnostic, or treatment decisions without validation against a verified, real-world clinical dataset.

