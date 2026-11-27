# Data Dictionary - Analysis Panel

> Variable-by-variable catalog of the analysis-ready state x quarter
> panel. This is the reference you check when a column name is ambiguous
> or you've forgotten what `rate_gap` is measured in.

**Unit of Observation:** one row per **state x quarter**. **2,601 rows** over entire quarterly panel (50 states + D.C. x 51 quarters, 2013-Q1 through 2025-Q3). **1,887 rows** for Model A listings dataset (50 states + D.C. x 51 quarters, 2016-Q3 through 2025-Q3).

---

## Identifiers

| Column | Type | Definition | Example | Source | Notes |
| --- | --- | --- | --- | --- | --- |
| `state` | object | 2-letter state abbreviation | CA | All | Non |
| `qdate` | object | Quarter start date (datetime) | 2013-01-01 | Constructed | Non |
| `quarter_str` | object | Quarter label | 2013Q1 | FHFA | Is the original data at the quarter level? |
| `ave_intrate` | float | Avg outstanding mortgage rate (%) | 5.2 | FHFA | How was the average obtained? |
| `pct_lt3` through `pct_ge6` | float | Rate distribution buckets (%) | 3.2 | FHFA | How was this captured? |
| `share_locked_in` | float | % mortgages below 5% rate | 48.599999999999994 | Derived (FHFA) | How was this captured? |
| `tot_loans` | float | Total outstanding loans (1000s) | 6322.0 | FHFA | How was this captured and is it already in 1000s or does the displayed value have to be transformed? |
| `mortgage_rate_30yr` | float | Quarterly avg 30-yr rate (%) | 3.503833333333333 | FRED | What execaptly is this? |
| `rate_gap` | float | Current rate minus outstanding rate (pp) | -1.696166666666667 | Derived | If negative ... if positive ... |
| `permits` | float | Quarterly building permits (sum) | 18221.19515546409 | Census/FRED | why is the sum 0....? |
| `ln_permits` | float | ln(1 + permits) | 9.81039564409814 | Derived | what does the log tell us in this case? |
| `hpi` | float | FHFA House Price Index | 407.27 | FHFA/FRED | how is the hpi calculated? |
| `hpi_yoy` | float | HPI year-over-year growth (%) | 6.89220755360751 | Derived | The year over year ... |
| `unemp_rate` | float | Quarterly avg unemployment rate (%) | 9.5 | BLS/FRED | how was this captured? |
| `zhvi` | float | Zillow Home Value Index ($) | 308943.13836837694 | Zillow | how is this captured? |
| `zhvi_yoy` | float | ZHVI year-over-year growth (%) | 11.036099494536899 | Derived | The year over year ... |
| `new_listing_count` | float | Quarterly new listings (sum) | 133590.0 | Realtor.com | Are there any values that are actual floast? |
| `active_listing_count` | float | End-of-quarter active inventory | 83653.0 | Realtor.com | how is this captured? |
| `median_days_on_market` | float | Quarterly avg days on market | 47.0 | Realtor.com | How is this captured? |
| `median_listing_price` | float | Quarterly avg listing price ($) | 504815.6666666667 | Realtor.com | How is this captured? |
| `ln_new_listings` | float | ln(1 + new listings) | 11.802538172546079 | Derived | what does this tell us? |
| `net_migration_lag1` | float | Lagged net domestic migration (per 1,000) | -2.067878797 | Census | how was this captured and why lagged?|
| `covid_dummy` | integer | 1 if 2020 Q2-Q3, else 0 | 0 | Constructed | why covid dummy? |
| `post_2022` | integer | 1 if 2022 Q2+, else 0 | 0 | Constructed | why post 2022 dummy? |
