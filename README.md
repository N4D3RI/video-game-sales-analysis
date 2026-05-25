# Video Game Sales Analysis

Exploratory data analysis and hypothesis testing on 16,700+ video game records (1980–2016) to identify the patterns that drive commercial success and inform a 2017 advertising plan for a fictional online retailer, *Ice*.

This project was completed as the Sprint 6 integrated case study in the TripleTen Data Science / ML program and was reviewed and approved by the program's review team.

---

## Project Goal

Acting as an analyst for the online store *Ice*, identify which factors (platform, genre, ratings, region) determine whether a game becomes a commercial success, and use those findings to recommend where the company should focus its 2017 ad spend.

## Dataset

- Source file: `games.csv` (provided by TripleTen) — 16,715 rows, 11 columns
- Fields: `Name`, `Platform`, `Year_of_Release`, `Genre`, `NA_sales`, `EU_sales`, `JP_sales`, `Other_sales`, `Critic_Score`, `User_Score`, `Rating`
- Time range: 1980 – 2016
- Note: the raw dataset is not redistributed in this repo (it's TripleTen course material). The notebook references it as `/datasets/games.csv`.

## Workflow

1. **Data preparation** — lowercased column names, coerced `User_Score` ("tbd" → NaN), kept `Year_of_Release` as nullable Int64, dropped rows missing both name and genre, computed `total_sales = NA + EU + JP + Other`, labelled missing ratings as `Unknown`.
2. **Period selection** — examined the platform lifecycle and selected **2013–2016** as the relevant period for forecasting 2017, since older console generations had effectively died off.
3. **Platform analysis** — ranked platforms by total sales in the relevant period, traced their growth/decline trajectories, and used boxplots to compare per-game sales distributions.
4. **Score vs. sales** — measured the correlation between `Critic_Score` / `User_Score` and `total_sales` for the leading platform, then compared the same relationship across other platforms.
5. **Genre analysis** — ranked genres by total sales and median per-game sales to separate high-volume genres from genres that just have lots of titles.
6. **Regional profiles** — built per-region top-5 platform and top-5 genre tables (NA, EU, JP) with full-region totals as the denominator, and looked at how ESRB rating correlates with sales by region.
7. **Hypothesis testing** — two two-sample Welch's t-tests on the 2013–2016 data:
   - H0: average user rating is the same for Xbox One and PC.
   - H0: average user rating is the same for Action and Sports genres.

## Key Findings

- The 2013–2016 era was dominated by **PS4** and **Xbox One**, with **3DS** holding strong in Japan.
- **Critic score** has a modest positive correlation with sales (~0.3–0.4 on PS4); **user score** has essentially **no** correlation with sales.
- Genre dominance is heavily region-dependent: shooters and sports drive sales in NA/EU, role-playing games dominate in JP.
- Hypothesis tests (Welch's t, α = 0.05): **reject** equal mean user score for Xbox One vs PC; **fail to reject** equal mean user score for Action vs Sports.
- Recommendation: 2017 ad spend should concentrate on PS4 + Xbox One in NA/EU, 3DS in JP, with weight on highly-rated shooter/sports titles in the West and RPGs in Japan.

## Stack

Python 3, pandas, NumPy, Matplotlib, seaborn, SciPy (stats), Jupyter Notebook.

## Files

- `notebook.ipynb` — full analysis, code, plots, and conclusions
- `requirements.txt` — pinned versions of the libraries used
- `README.md` — this file

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook notebook.ipynb
```

The notebook expects the dataset at `/datasets/games.csv`. Update the `pd.read_csv(...)` call in the data-loading cell if your dataset lives somewhere else.

## Status

Reviewed and approved by TripleTen's review team (May 2026).
