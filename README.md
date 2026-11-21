# Vehicle Fuel Usage & Driver Behaviour Analysis

Exploratory data analysis, data cleaning, and feature engineering on **1.17M+ global vehicle refuelling logs** to uncover cross-market refuelling trends, fleet demographics, and user growth patterns.

## Project Overview
Real-world telematics and user-logged vehicle datasets contain high volumes of missing records, inconsistent units, and data-entry anomalies. This project builds a reproducible cleaning and validation pipeline in Python to recover incomplete entries, standardise measurements across international currencies, and extract behavioural insights.

## Data Cleaning & Feature Engineering Pipeline
* **Temporal Validation & Imputation:** Parsed `date_fueled` entries (identifying **7.82%** malformed records) and imputed missing/invalid timestamps using `date_captured` proxies within a valid 2005–2026 window.
* **Domain-Equation Recovery:** Recovered **87.55%** missing `miles` entries alongside missing `gallons`, `mpg`, `total_spent`, and `cost_per_gallon` values using mathematical relationships ($\text{Miles} = \text{MPG} \times \text{Gallons}$ and $\text{Total Spent} = \text{Cost per Gallon} \times \text{Gallons}$).
* **Regex Metadata Extraction:** Extracted currency symbols (used as regional/country proxies) and parsed vehicle manufacturer, model, model year, and unique `user_id` fields from raw `user_url` strings.
* **Metric Standardisation:** Converted imperial measurements into metric units (`km_driven`, `litres_filled`, and `litres_per_100km`) for international comparability.
* **Currency-Specific Outlier Filtering:** Applied physical boundaries ($5 < \text{Litres} < 150$, $0 \le \text{Vehicle Age} \le 25$, $10 < \text{Odometer} < 500,000$) and market-specific financial thresholds across the top five currencies (`$`, `£`, `€`, `CA$`, `R`), isolating **359,234 (~37%)** implausible entries and retaining **612,844** validated records.

## Key Insights
* **Data Recovery:** Mathematical imputation preserved over **1.10 million** usable observations that would otherwise have been discarded due to missing mileage fields.
* **User Growth Surge:** Daily active user tracking revealed a sharp acceleration in app engagement between **2020 and 2023** (peaking near ~2,500 unique daily users), reflecting heightened driver focus on fuel-cost tracking.
* **Market & Fleet Distribution:** Activity is concentrated across five primary currency markets (US, UK, Eurozone, Canada, and South Africa), with **Ford** (14,352 unique users) and **Toyota** (13,409 unique users) representing the largest vehicle cohorts.

## Tech Stack
* **Language:** Python
* **Libraries:** Pandas, NumPy, Matplotlib, Seaborn, Regular Expressions (`re`)

## Repository Structure
* `analysis.ipynb` — Full Jupyter Notebook containing data inspection, cleaning, feature engineering, outlier filtering, and visualisations.
* `DVE.pdf` — Full technical report (co-authored with Ntokozo Skosana) covering the complete statistical analysis, South African fuel price-adjustment behaviour
