# Wage Polarization and AI: Honors Thesis Project

## Overview
This repository contains the data processing, integration, and analysis code for **“Wage Polarization and AI: Empirical Evidence from U.S. Labor Market Data”**, an honors thesis completed for *ECON 495* at the University of Southern California.  

The project investigates how **AI exposure influences wage inequality across U.S. occupations** between 2015 and 2024, using large-scale data from the *Bureau of Labor Statistics (BLS)* and the *O*NET* database.  

While the thesis itself explores the economic implications of automation and inequality, this repository focuses on the **data engineering and analytical workflow** behind the study — from cleaning and merging heterogeneous datasets to producing reproducible regression and visualization outputs.

---

## Data Pipeline Summary

The full data workflow integrates several public datasets to construct an occupation-level panel for empirical analysis:

1. **O*NET Automation and Job Zone Data**  
   - Source: U.S. Department of Labor’s Employment and Training Administration (O*NET 27.4)  
   - Provides *Degree of Automation* and *Job Zone* scores used to quantify automation risk.

2. **BLS Occupational Employment and Wage Statistics (OEWS)**  
   - Annual occupation-level wages (2015–2024).  
   - Cleaned and merged with O*NET to estimate the relationship between automation exposure and wages.

3. **BLS Current Population Survey (CPS)**  
   - Median weekly earnings and employment shares by gender, race, and age.  
   - Used for descriptive demographic analysis.

4. **FRED Consumer Price Index (CPI)**  
   - Used to deflate nominal wages into real wages for cross-year comparability.

5. **Crosswalks and Code Mappings**  
   - SOC 2010 → 2018 → 2019 crosswalks to align occupational codes between CPS, OEWS, and O*NET.  
   - Title normalization routines handle inconsistent punctuation and “all other” categories.

---

## Repository Structure

```
Honors_Thesis_Project/
│
├── data/                         # Raw and processed input data
│   ├── 1_updated_median_weekly_income/
│   ├── 2_updated_median_weekly_income/
│   ├── median_weekly_income/
│   ├── demographic_factors/
│   ├── OEWS/
│   └── SOC/
│
├── code/                         # Main analysis notebooks (Python)
│   ├── 1_merge_income_demo.ipynb
│   ├── 1_updated_median_weekly_income.ipynb
│   ├── 2_merge_income_automation_level.ipynb
│   ├── 3_merge_analyze_OEWS.ipynb
│   ├── 4_CPS.ipynb
│   ├── table_analysis/
│   └── output/
│
├── Readings/                     # Supporting literature and notes
│
└── README.md                     # (this file)
```

---

## Code Workflow

Each notebook within `occupation_Analysis/` corresponds to a specific stage of the pipeline:

| Notebook | Purpose |
|-----------|----------|
| **1_merge_income_demo.ipynb** | Reads and merges raw CPS income and demographic datasets. |
| **1_updated_median_weekly_income.ipynb** | Cleans and standardizes income data by year and occupation. |
| **2_merge_income_automation_level.ipynb** | Integrates automation scores from O*NET with wage data (OEWS × O*NET merge). |
| **3_merge_analyze_OEWS.ipynb** | Performs regression analysis to estimate relationships between automation risk, skill level, and wages. |
| **4_CPS.ipynb** | Generates demographic summary statistics and automation-exposure distributions by gender, race, and age. |

All scripts rely on **pandas**, **numpy**, and **matplotlib/seaborn** for data handling and visualization.  
---

## Outputs

- Cleaned, merged CSVs for regression analysis  
- Summary tables and charts for wage trends by automation risk and demographic group  
- Reproducible Jupyter notebooks that generate final figures for the thesis paper  
