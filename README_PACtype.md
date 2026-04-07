# Physical Activity Trends by selected cancer types in BRFSS, 2018–2024
This repository contains the code for the paper entitled "Trends in Physical Activity by Cancer History in a Nationally Representative Sample of U.S. Adults"

The analysis addresses four primary aims

1. **Prevalence Estimation** — Survey-weighted annual prevalence of physical activity by cancer type.
2. **Trend Analysis** — Annual percentage change (APC) in physical activity prevalence over time.
3. **Adjusted Prevalence Differences** — Adjusted differences in physical activity between each cancer type group and adults with no cancer history.

---

## Files Included
- `PACtype.Rmd`: R Markdown file containing annotated code used to run the above analysis
- `README(PACtype).md`: This file

---

## Data Source
This analysis uses annual public-use data files from the [CDC Behavioral Risk Factor Surveillance System (BRFSS)](https://www.cdc.gov/brfss/annual_data/annual_data.htm). BRFSS is an ongoing state-based telephone survey of non-institutionalized U.S. adults that uses a complex, stratified, multistage probability sampling design.

### Required Files
Download the following XPT files from the CDC BRFSS website and save them using the **exact filenames** listed below:


---


## Required Data Files

This analysis requires both **main** and **versioned** (V1, V2, V3) BRFSS release files for years in which the cancer type module was administered. Download all files from the [CDC BRFSS website](https://www.cdc.gov/brfss/annual_data/annual_data.htm).

Only states listed in Supplementary Table 2 of the manuscript are retained during import. The table below lists every file used and which states it supplies.

| Year | File | States Used |
|------|------|-------------|
| 2018 | `LLCP2018.XPT` | DE, IN, MI, MO, NJ, SD |
| 2018 | `LLCP18V2.XPT` | KS |
| 2019 | `LLCP2019.XPT` | WY |
| 2019 | `LLCP19V2.XPT` | MD, MA |
| 2020 | `LLCP2020.XPT` | AZ, CT, DE, GA, GU, HI, IN, LA, MA, MI, MS, MO, MT, NJ, NM, NC, RI, SD, UT, VT, VA, WI |
| 2020 | `LLCP20V1.XPT` | KS, ME, NE, NY, OH, OK |
| 2020 | `LLCP20V2.XPT` | MD |
| 2020 | `LLCP20V3.XPT` | NY *(weight rescaled — see Step 2)* |
| 2021 | `LLCP2021.XPT` | AR, DE, HI, MI, MT, NJ, NM, PR, UT, WI |
| 2021 | `LLCP21V1.XPT` | NE, OK |
| 2021 | `LLCP21V2.XPT` | KS |
| 2021 | `LLCP21V3.XPT` | MD |
| 2022 | `LLCP2022.XPT` | AR, CO, CT, DE, HI, ID, IL, IN, MI, MO, NE, NV, NJ, NM, NC, OR, PR, RI, SD, UT, VT, VA, WI |
| 2022 | `LLCP22V1.XPT` | IA, MA, OH, OK |
| 2022 | `LLCP22V2.XPT` | AZ, KS |
| 2022 | `LLCP22V3.XPT` | MD |
| 2023 | `LLCP2023.XPT` | CT, GA, IL, IN, MI, MN, MS, NH, NJ, TN, USVI, VA, WV, WI |
| 2023 | `LLCP23V1.XPT` | NY, OK |
| 2023 | `LLCP23V2.XPT` | KS, MD |
| 2024 | `LLCP2024.XPT` | CT, DE, GA, IN, MA, MI, MO, NJ, NC, SD, UT, USVI, VA |
| 2024 | `LLCP24V1.XPT` | AZ, KS |
| 2024 | `LLCP24V2.XPT` | NE, NY |

> The import code references all filenames exactly as listed. Update paths in the script if your filenames differ.

## Data Structure

BRFSS data are distributed across multiple annual release files. Each year may include a **main file** and up to three versioned files (V1, V2, V3), each carrying a different final weight variable:

| File Type | Weight Variable |
|-----------|----------------|
| Main      | `_LLCPWT`      |
| V1        | `_LCPWTV1`     |
| V2        | `_LCPWTV2`     |
| V3        | `_LCPWTV3`     |



## Required Packages

```r
pacman::p_load(haven,dplyr,tidyr,tibble,survey,broom,ggplot2,scales,knitr,stringr)
```


## Outputs

| Output | Description |
|---|---|
| `prev_all_types` | Annual weighted PA prevalence by cancer type (Supplementary Table 4) |
| `apc_type_results` | APC estimates with 95% CIs by cancer type (Table 2) |
| `apd_type_results` | Adjusted prevalence differences vs. no cancer history (Supplementary Table 5) |
| `Fig_Breast_vs_NoCancer.png` | PA trend — breast cancer vs. no cancer history (females) |
| `Fig_Prostate_vs_NoCancer.png` | PA trend — prostate cancer vs. no cancer history (males) |
| `Fig_Colon_vs_NoCancer.png` | PA trend — colon cancer vs. no cancer history |
| `Fig_Other_vs_NoCancer.png` | PA trend — other cancers vs. no cancer history |

---

## Notes

- All estimates are **survey-weighted** and account for the complex multistage BRFSS sampling design.
- The analytic sample is restricted to states that administered the **optional cancer type module**, which varies by year.
- Cancer type is only ascertained among respondents who reported a cancer history; all others have `NA` for cancer type by design.
- APC models are fit to **aggregated annual prevalence estimates**, not individual-level data.
- The complete-case approach used here excludes respondents with missing values on any analytic variable. 

## Author
- Name: Biruk Demma
- Email: b.d.demma@wustl.edu
- Date: April 2026

