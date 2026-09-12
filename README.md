# Wage Polarization and AI: Empirical Evidence from U.S. Labor Market Data

Honors thesis, Department of Economics, University of Southern California (ECON 495), submitted May 2025. This repository holds the data pipeline and the analysis notebooks behind the thesis: an occupation-level panel built from the Bureau of Labor Statistics and O\*NET, and the regressions estimated on it. The thesis document itself is not in this repository.

## What the thesis does

- Builds an occupation × year panel for 2015–2024 from BLS Occupational Employment and Wage Statistics (OEWS), merged with O\*NET's Degree of Automation rating and Job Zone.
- Deflates wages to real terms with the BLS CPI-U.
- Estimates the association between automation exposure and wages with **OLS** (baseline and stratified by Job Zone), **quantile regression** at the 10th, 50th and 90th percentiles, and a **difference-in-differences** specification around 2023.
- Adds a descriptive analysis on Current Population Survey data of how exposure falls across gender, race and age.

Headline finding as submitted: automation exposure is positively associated with wages, and the association is concentrated in high-skill occupations.

## Where each estimate lives

| Estimate | Notebook and cell | Output |
|---|---|---|
| OLS baseline, and one OLS per Job Zone | `occupation_Analysis/3_merge_analyze_OEWS.ipynb`, cells 11 and 14 | `occupation_Analysis/Model Stats/` |
| Difference-in-differences: pooled, with Job Zone dummies, and per zone | same notebook, cells 18, 20 and 47 | `Model Stats/DiD_*` |
| Quantile regression, q = 0.1 / 0.5 / 0.9, with and without year effects | same notebook, cells 27 and 29 | `Model Stats/` |
| CPS descriptive figures | `occupation_Analysis/4_CPS.ipynb` | `occupation_Analysis/output/4_CPS/` |
| CPS → SOC → O\*NET crosswalk | `occupation_Analysis/2_merge_income_automation_level.ipynb` | `output/final_merged_income_automation_2015_2024.xlsx` |

Run the notebooks from `occupation_Analysis/`. They need pandas, numpy, statsmodels, matplotlib and seaborn.

## Data (all public)

| Source | Used for | Where |
|---|---|---|
| BLS OEWS, national, May 2015–2024 | the wage panel | `occupation_Analysis/OEWS/` |
| BLS CPS Table 39 plus the age and race tables | median weekly earnings by occupation and demographic group | `occupation_Analysis/1_updated_median_weekly_income/`, `data/` |
| O\*NET 27.4 Degree of Automation and Job Zone (USDOL/ETA, CC BY 4.0) | the exposure measure | `occupation_Analysis/ONET_Degree_of_Automation.csv` |
| BLS CPI-U | the deflator | `occupation_Analysis/CPI/` |
| Census and SOC classification lists, 2010 → 2018 SOC and 2019 O\*NET-SOC crosswalks | aligning occupation codes across years | `occupation_Analysis/SOC/` |

## Status and limitations

This is version 1, the code as submitted in May 2025, kept unchanged. A 2026 revision is in progress and will be added alongside it with a note on what changed, rather than replacing it.

What the revision addresses, in order of importance:

1. **The difference-in-differences design does not identify what it is meant to.** The treatment variable is O\*NET's Degree of Automation, one 2019 rating carried unchanged across all ten years, so it cannot stand for a 2023 shock; every occupation carries a score, so there is no untreated comparison group; and the specification has neither occupation fixed effects nor clustered standard errors. The thesis's own "Areas of Improvement" section already notes the first of these. The interaction coefficient should be read as unidentified rather than as evidence of no effect.
2. **The quantile regressions stop at the solver's iteration limit** at q = 0.5 and q = 0.9, so those coefficients need re-estimating to convergence before they are quoted.
3. **The OEWS ↔ O\*NET merge uses cleaned occupation titles, not SOC codes.** The proper crosswalk already exists in notebook 2 and is not applied in the regression notebook; the revision rebuilds the panel on it.
4. Smaller fixes travelling with the revision: the CPI entry used for 2024, and a hardcoded local path at the top of the regression notebook.

## Changelog

- **2026-09-11** Full review of the five notebooks; findings recorded outside this repository. No v1 code changed.
- **2026-09-12** README rewritten to map each estimate to the cell that produces it and to state the limitations above. Removed `Readings/`, a folder of published papers by other authors that should not be redistributed here. Stopped tracking `.DS_Store` and Office lock files.
