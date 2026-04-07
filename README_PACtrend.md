# Physical Activity Trends by Cancer History in BRFSS, 2018–2024
This repository contains the code for the paper entitled "Trends in Physical Activity by Cancer History in a Nationally Representative Sample of U.S. Adults"

The analysis addresses four primary aims

1. Estimate annual survey-weighted prevalence of PA by cancer history (2018–2024)
2. Assess temporal trends using annual percentage change
3. Estimate adjusted prevalence differences in PA by cancer history and cancer type
4. Examine aerobic PA guideline adherence (≥150 min/week) in 2019 and 2023

---

## Files Included
- `PACtrend.Rmd`: R Markdown file containing annotated code used to run the above analysis
- `README.md`: This file

---

## Data Source
This analysis uses annual public-use data files from the [CDC Behavioral Risk Factor Surveillance System (BRFSS)](https://www.cdc.gov/brfss/annual_data/annual_data.htm). BRFSS is an ongoing state-based telephone survey of non-institutionalized U.S. adults that uses a complex, stratified, multistage probability sampling design.

### Required Files
Download the following XPT files from the CDC BRFSS website and save them using the **exact filenames** listed below:

| Year | Filename |
|------|----------|
| 2018 | `LLCP2018.XPT` |
| 2019 | `LLCP2019.XPT` |
| 2020 | `LLCP2020.XPT` |
| 2021 | `LLCP2021.XPT` |
| 2022 | `LLCP2022.XPT` |
| 2023 | `LLCP2023.XPT` |
| 2024 | `LLCP2024.XPT` |

> *Note:* The import code references these filenames exactly. If your filenames differ, update the file paths in the import section of the script before running.

---

## How to Run

1. Download the seven BRFSS `.XPT` files listed above.
2. Place them in the same folder as `PACtrend.Rmd`.
3. Open `PACtrend.Rmd` in RStudio.
4. Run code chunks sequentially, or click **Knit** to render the full document.

### Prerequisites
- R (≥ 4.0 recommended)
- RStudio
- The following R packages:
```r
install.packages(c(
  "haven",
  "dplyr",
  "tidyr",
  "tibble",
  "ggplot2",
  "survey",
  "broom",
  "gtsummary",
  "knitr",
  "pacman"
))
```
---

## Analytic Methods
All weighted analyses account for BRFSS's complex survey design using the `survey` R package. Annual survey-weighted PA prevalence estimates are modeled using log-linear regression with survey year as a continuous predictor. Results are reported as annual percentage change (APC) with 95% confidence intervals. Survey-weighted linear probability models (Gaussian family, identity link) are used to estimate adjusted prevalence differences (aPDs) comparing adults with vs. without a cancer history. Models are adjusted for age group, sex, race/ethnicity, educational attainment, health insurance, personal health care provider, marital status, smoking status, and survey year.

- For breast cancer analyses: restricted to female respondents
- For prostate cancer analyses: restricted to male respondents

---

### Outputs from the script

#### Main Outputs

| Output | Description |
|--------|-------------|
| **Table 1** | Unweighted participant characteristics by cancer history |
| **Figure 1** | Annual weighted PA prevalence by cancer history, 2018–2024 |
| **Table 2** | APC estimates by cancer history and cancer type |
| **Table 3** | Weighted prevalence of meeting the aerobic PA guideline in 2019 and 2023 |

The main figure is saved as:

```
Fig1_PA_trend_cancer_history.png
```

#### Supplemental Outputs from the script

| Output | Description |
|--------|-------------|
| Data for Supplementary Figure 1 | Flow diagram of dataset derivation (primary and secondary datasets) |
| Supplementary Figure 2 | PA prevalence trends by cancer type vs. no cancer history |
| Data for Supplementary Tables 3A and 3C | Missing data summaries |
| Data for Supplementary Table 4 | Annual weighted PA prevalence by cancer history|
| Data for Supplementary Table 5 | Adjusted prevalence differences by cancer history|

---

### Software

All analyses were conducted in **R (version 4.5.1)** using the `survey` package (version 4.4.8).

---
### Author
- Name: Biruk Demma
- Email: b.d.demma@wustl.edu
- Date: April 2026
