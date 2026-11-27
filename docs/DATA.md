# Data - Sources, Lineage & Dictionary

> What came from where, how it was harmonized, and what to distrust.

---

## Panel at a glance

| Property | Value |
|--- | --- | --- |
| Unit of observation | State (50 + DC = 51) |
| Time | Quarter |
| Span | Listings analysis (Model A): 2016 Q3 - 2025 Q3; Building permits analysis (Model B): 2013 Q1 - 2025 Q3 |
| Frequency harmonization | Monthly series → quarterly |
| Binding coverage constraint | Realtor.com listings start 2016 Q3 |
| Observations | Model A, C → 1,887 (model A dataset); Model B → 2,601 (model B dataset); Robustness Check 1, 2, 4 → 1,887 (quarterly panel with specific robustness check modifications; similar to model A dataset); Robustness Check 3 → 962 (quarterly panel with specific modifications; similar to model A dataset but with analysis only on the high and low lock-in states) ; Robustness Check 5 → 714 (model r5 dataset), Robustness Check 6 → 1836 (quarterly panel with specific modifications; similar to model A but dropped first row per state for the first differenced model)|

---

## Sources → variables

| Dataset | Source | Frequency | Coverage |
|---------|--------|-----------|----------|
| Outstanding mortgage statistics | FHFA National Mortgage Database | Quarterly | 50 states + DC, 2013 Q1 – 2025 Q3 |
| Building permits | Census Bureau / FRED | Monthly → Quarterly | 50 states + DC, 2000/01 – 2025/12 |
| House Price Index | FHFA / FRED | Monthly → Quarterly | 50 states + DC, 2000/01 – 2025/10 |
| Unemployment rate | BLS / FRED | Monthly → Quarterly | 50 states + DC, 2000/01 –2025/12 |
| 30-year mortgage rate | Freddie Mac / FRED | Monthly → Quarterly | National, 2000/01 – 2025/12 |
| Home values (ZHVI) | Zillow Research | Monthly → Quarterly | 50 states + DC, 2000/01 – 2026/02 |
| New listings & inventory | Realtor.com | Monthly → Quarterly | 50 states + DC, 2016/07 – 2026/02 |
| Net domestic migration | Census Bureau | Annual (lagged 1yr) | 50 states + DC, 2010–2025 |