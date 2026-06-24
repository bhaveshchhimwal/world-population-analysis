# Global Population Analysis

An exploratory data analysis and demographic segmentation of 234 countries, using 2024 UN-style population data. Built as a data analyst portfolio project — focus is on asking specific, business-relevant questions rather than generic exploration.

## Objective

Most population datasets get treated as a sandbox for plotting practice. This project instead asks four concrete questions:

1. Where is the world's population concentrated, and where is it growing fastest?
2. Is population density related to urbanization?
3. What do net migration patterns reveal about labor movement and displacement?
4. Can countries be meaningfully segmented into demographic groups without using region or income labels?

## Key Findings

- **Population is heavily concentrated.** India and China alone account for more people than the next 13 most populous countries combined.
- **Size and growth rate are independent.** The fastest-growing countries (Chad, Oman, Syria, South Sudan) are driven by high fertility or post-conflict population shifts — not economic expansion. The fastest-shrinking are mostly small island nations plus Greece, driven by emigration.
- **Density and urbanization are nearly uncorrelated (r = 0.116).** A country can be sparse overall but highly urbanized (Australia), or moderately dense with a large rural population (India) — these measure different things.
- **Migration splits into two distinct mechanisms.** Labor migration toward traditional destination economies (US, UK, Canada, UAE) versus returning displaced populations in post-conflict countries (Ukraine, Syria).
- **Unsupervised clustering recovers the demographic transition model.** K-Means (k=4, chosen via the elbow method) on growth rate, density, fertility, median age, and urbanization — with no regional or economic labels provided — separates countries into Young & Fast-Growing (concentrated in sub-Saharan Africa), Transitioning, and Mature & Slow-Growing (concentrated in Europe and East Asia) groups, plus Macao as a single-country extreme outlier.

## Tools

- **pandas / NumPy** — data cleaning and transformation
- **Matplotlib / Seaborn** — visualization
- **scikit-learn** — `StandardScaler`, `KMeans` for clustering

## Data

Source: [World Population by Countries (2025), Kaggle](https://www.kaggle.com/datasets/samithsachidanandan/world-population-by-countries-2025). 234 countries/territories, 12 original columns (population, growth rate, net change, density, land area, net migrants, fertility rate, median age, urban population %, world share).

## Approach

1. **Cleaning** — converted comma-formatted numeric strings, stripped `%` symbols from rate columns, and handled `N.A.` values (concentrated in small territories like Monaco and Hong Kong) as missing rather than imputed.
2. **EDA** — answered each question above with a targeted visualization (log-scaled where population/density skew required it) and a calculated statistic (e.g., correlation coefficient) rather than relying on visual impression alone.
3. **Clustering** — selected rate-based features (excluding raw population/land area to avoid clustering by sheer size), scaled with `StandardScaler`, and used the elbow method to justify k=4 rather than choosing it arbitrarily.

## Files

- `world_population_analysis.ipynb` — full analysis notebook
- `Wolrd_Population_Data.csv` — source data

## Notes

`Urban Pop %` had 18 missing values, concentrated almost entirely in small territories and city-states (Hong Kong, Monaco, Réunion, etc.) plus Venezuela. These were left as `NaN` rather than dropped or imputed, since the missingness pattern wasn't random and a fabricated average would misrepresent these unusual cases.

## Live Dashboard

An interactive Tableau Public dashboard built from this same cleaned dataset is available here: [link](https://public.tableau.com/app/profile/bhavesh.chhimwal/viz/Dashboard_17823029131070/Dashboard1)
