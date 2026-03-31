# Mortgage Rate Lock-In Effect: A State-Level Analysis of U.S. Housing Supply

**How the gap between current mortgage rates and homeowners' existing rates is freezing the U.S. housing market — and which states are hit hardest.**

---

## Overview

When mortgage rates surged from ~3% to ~7% in 2022, roughly 60 million American homeowners found themselves locked into rates far below the current market. Selling their home would mean giving up a 3% mortgage and taking on a 7% one — a penalty of **$654/month** on a typical $400,000 home. The rational response: don't sell.

This project measures that lock-in effect econometrically, estimating how much it suppresses housing supply across all 50 states and the District of Columbia. Using a quarterly panel dataset (2013–2025) combining data from the FHFA, Census Bureau, BLS, Zillow, and Realtor.com, the analysis identifies:

- **How large the lock-in effect is:** A 1 percentage point increase in the rate gap reduces new listings by **9.3%** (p < 0.001)
- **Which states are hit hardest:** Connecticut (-21.6%), Rhode Island (-17.6%), Minnesota (-17.3%) lead the severity ranking
- **Which states are least affected:** Texas (-2.2%), Tennessee (-2.5%), Arkansas (-2.8%) — large, liquid Sun Belt markets
- **Whether it spills over to new construction:** It does not. Building permits are unaffected (p = 0.93)
- **The national scale:** Approximately **1 million fewer listings per year** compared to a zero-gap counterfactual

## Key Findings

### The Lock-In Is Real, Universal, and Statistically Robust

| Finding | Detail |
|---------|--------|
| **50 of 51 states** show negative lock-in coefficients | DC is the sole exception (structural outlier) |
| **48 of 51 states** are significant at the 5% level | Only TN, SD, TX are marginally insignificant |
| Effect survives **6 robustness checks** | Alternative IVs, boom controls, first-differencing, subsample restriction |
| Lock-in operates through **existing homes only** | No detectable effect on building permits |
| Effect is **independent** of the pandemic boom | Coefficient unchanged after controlling for boom intensity |
| **Unit root concern addressed** | First-differenced model confirms results (β = -0.047, p < 0.001) |

### State Severity Ranking (Top 13 — "Severe" Tier)

| Rank | State | Coefficient | Interpretation |
|------|-------|-------------|----------------|
| 1 | CT | -0.216 | 1 pp increase → 21.6% fewer listings |
| 2 | RI | -0.176 | 1 pp increase → 17.6% fewer listings |
| 3 | MN | -0.173 | 1 pp increase → 17.3% fewer listings |
| 4 | MD | -0.169 | 1 pp increase → 16.9% fewer listings |
| 5 | NJ | -0.168 | 1 pp increase → 16.8% fewer listings |
| 6 | MA | -0.158 | 1 pp increase → 15.8% fewer listings |
| 7 | NH | -0.155 | 1 pp increase → 15.5% fewer listings |
| 8 | IL | -0.150 | 1 pp increase → 15.0% fewer listings |
| 9 | ME | -0.148 | 1 pp increase → 14.8% fewer listings |
| 10 | VT | -0.145 | 1 pp increase → 14.5% fewer listings |
| 11 | NM | -0.139 | 1 pp increase → 13.9% fewer listings |
| 12 | VA | -0.133 | 1 pp increase → 13.3% fewer listings |
| 13 | PA | -0.124 | 1 pp increase → 12.4% fewer listings |

The full 51-state ranking with confidence intervals is available in `output/regression/state_lockin_ranking.csv`.

---

## Methodology

### Core Variable: Rate Gap

```
RateGap_it = MORTGAGE30US_t − AVE_INTRATE_it
```

The difference between the current 30-year mortgage rate and the average outstanding mortgage rate in state *i* at quarter *t*. Sourced from Freddie Mac (current rate) and FHFA's National Mortgage Database (outstanding rates by state).

### Primary Model (Model A)

```
ln(NewListings_it) = β₁(RateGap_it) + β₂(HPI_YoY_it) + β₃(UnempRate_it)
                   + β₄(MedianDOM_it) + β₅(NetMigration_it₋₁) + β₆(COVID_t)
                   + αᵢ + εᵢₜ
```

- **αᵢ:** State fixed effects (absorb time-invariant state characteristics)
- **Standard errors:** Clustered by state
- **Panel:** 51 states × 37 quarters (2016 Q3 – 2025 Q3), N = 1,887

### Model Suite

| Model | Purpose | Key Result |
|-------|---------|------------|
| **A** (Primary) | Aggregate lock-in effect on listings | β = -0.093, p < 0.001 |
| **B** (Secondary) | Spillover to building permits | β = -0.001, p = 0.929 (null) |
| **C** (Heterogeneous) | 51 state-specific coefficients | 50/51 negative, 48/51 significant |
| **R1** | Alternative IV: share of mortgages < 5% | β = -0.013, p < 0.001 |
| **R2** | Monotonic gradient: 5 rate buckets entered separately | Directionally correct |
| **R3** | Diff-in-diff: top vs bottom quartile | Null (binary design lacks power) |
| **R4** | Pandemic boom confound control | β unchanged at -0.092 |
| **R5** | Post-2022 subsample only | β = -0.223, p < 0.001 |
| **R6** | First-differenced (addresses unit roots) | β = -0.047, p < 0.001 |

---

## Data Sources

| Dataset | Source | Frequency | Coverage |
|---------|--------|-----------|----------|
| Outstanding mortgage statistics | FHFA National Mortgage Database | Quarterly | 51 states, 2013–2025 |
| Building permits | Census Bureau / FRED | Monthly → Quarterly | 51 states, 2000–2025 |
| House Price Index | FHFA / FRED | Quarterly | 51 states, 2000–2025 |
| Unemployment rate | BLS / FRED | Monthly → Quarterly | 51 states, 2000–2025 |
| 30-year mortgage rate | Freddie Mac / FRED | Monthly → Quarterly | National, 2000–2025 |
| Home values (ZHVI) | Zillow Research | Monthly → Quarterly | 51 states, 2000–2025 |
| New listings & inventory | Realtor.com | Monthly → Quarterly | 51 states, 2016–2025 |
| Net domestic migration | Census Bureau | Annual → Quarterly (lagged 1yr) | 51 states, 2011–2025 |

All data is publicly available. Raw files are stored in `data/raw/` and the assembled panel in `data/panel/`.

---

## Repository Structure

```
lockin_project/
├── data/
│   ├── raw/                          # Original downloaded CSVs (9 files)
│   └── panel/
│       ├── quarterly_panel.csv       # Assembled panel (2,601 rows × 28 cols)
│       ├── model_a_listings.csv      # Model A subset (1,887 obs)
│       ├── model_b_permits.csv       # Model B subset (2,601 obs)
│       └── model_r5_post2022.csv     # Post-2022 subset (714 obs)
│
├── notebooks/
│   ├── 01_pre_merge_eda.ipynb        # Raw data exploration & validation
│   ├── 02_panel_construction.ipynb   # Data cleaning, aggregation & merge
│   ├── 03_post_merge_eda.ipynb       # Analytical EDA (10 diagnostic plots)
│   ├── 04_regression.ipynb           # Primary models (A, B, C) + diagnostics
│   └── 05_robustness.ipynb           # Robustness suite (R1–R6)
│
├── output/
|   ├── eda/                          # Pre-merge EDA plots (8 PNGS)
│   ├── eda_post/                     # Post-merge EDA plots (10 PNGs)
│   ├── regression/
│   │   ├── model_ab_comparison.csv   # Side-by-side Model A vs B
│   │   ├── state_lockin_ranking.csv  # Full 51-state ranking
│   │   └── state_ranking_chart.png   # Severity visualization
│   ├── robustness/
|       ├── r2_monotonic_gradient.png
│       ├── robustness_comparison.csv # All models side-by-side
│       └── robustness_comparison_chart.png
|
├── scripts/
|   └── 01_fred_data_collection
│
└── README.md
```

---

## Reproducing the Analysis

### Requirements

```
Python 3.10+
pandas >= 2.0
numpy >= 1.24
matplotlib >= 3.7
seaborn >= 0.12
scipy >= 1.10
statsmodels >= 0.14
linearmodels >= 5.3
```

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/<username>/lockin-effect.git
cd lockin-effect

# 2. Run notebooks in order
#    00 → Pre-merge EDA (data validation)
#    01 → Panel construction (builds quarterly_panel.csv)
#    03 → Post-merge EDA (diagnostic plots)
#    04 → Primary regressions (Models A, B, C)
#    05 → Robustness checks (R1–R6)
```

All raw data files are included in `data/raw/`. No API keys or external downloads are required.

---

## Key Visualizations

### The Lock-In Emerges (2022)

The rate gap was **negative** throughout 2013–2021 (homeowners held above-market rates). It flipped positive in early 2022 and peaked at ~3 pp by late 2023 — creating a financial penalty of over $650/month for the typical homeowner who sells and rebuys.

> See: `output/eda_post/01_rate_gap_timeseries.png`

### State Severity Ranking

A color-coded bar chart of all 51 states ranked by lock-in severity, from Connecticut (-0.216) to DC (+0.092). States are grouped into four tiers: Severe, Moderate-High, Moderate-Low, and Mild.

> See: `output/regression/state_ranking_chart.png`

### Visual Diff-in-Diff

High lock-in states (top quartile) vs low lock-in states (bottom quartile) plotted over time. Both groups track together before 2022, then diverge — with the high lock-in group experiencing a sharper decline in listings.

> See: `output/eda_post/09_visual_did.png`

---

## Limitations

- **Entity FE only (no time FE) in primary specification.** Time fixed effects absorb the common rate gap movement, leaving insufficient variation for identification. The tradeoff is that national-level confounders (consumer sentiment, stock market effects) are uncontrolled. Model R5 (post-2022 subsample) partially addresses this.

- **Observational design.** The rate gap is not randomly assigned. States with larger gaps tend to be those that experienced bigger pandemic booms. Model R4 directly controls for this confound and shows the coefficient is unaffected.

- **Realtor.com coverage starts 2016 Q3.** The new listings dependent variable limits Model A to 37 quarters. Model B (permits) uses the full 51-quarter panel as a complement.

- **State-level aggregation.** Within-state heterogeneity (urban vs rural, coastal vs inland) is averaged over. MSA-level analysis would capture finer variation but requires additional data assembly.

- **Linear specification.** The relationship between rate gap and listings may be nonlinear (the lock-in may bite harder above some threshold). Model R2 partially addresses this but the monotonic gradient is imperfect.

---

## References

- Federal Housing Finance Agency. *National Mortgage Database: Outstanding Mortgage Statistics.* https://www.fhfa.gov/data/nmdb
- Freddie Mac. *Primary Mortgage Market Survey.* Via FRED: `MORTGAGE30US`
- U.S. Census Bureau. *Building Permits Survey.* https://www.census.gov/construction/bps
- Bureau of Labor Statistics. *Local Area Unemployment Statistics.* Via FRED
- Zillow Research. *Zillow Home Value Index (ZHVI).* https://www.zillow.com/research/data
- Realtor.com Research. *Inventory Core Metrics.* https://www.realtor.com/research/data
- Gyourko, J., Hartley, J.S., & Krimmel, J. (2021). "The Local Residential Land Use Regulatory Environment Across U.S. Housing Markets." *Journal of Urban Economics*, 124.

---

## License

This project is for academic and research purposes. All data is sourced from publicly available government and research platforms.
