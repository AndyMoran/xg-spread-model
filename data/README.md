# Data

## Source Files

Data files are not committed to this repository due to size. Reproduce them by running the notebooks in order.

### xG Data

Downloaded via the `understat` Python library from [Understat.com](https://understat.com).

Run `notebooks/01_data_pipeline.ipynb` Cell 1 to download.

| File | Description | Shape |
|---|---|---|
| `pl_match_xg_2015_2025.csv` | Raw Understat API output | (3800, ~20) |
| `pl_match_xg_clean.csv` | Parsed match-level xG and goals | (3800, 9) |
| `pl_team_match_spread.csv` | Team-level long format with spread series | (7600, 11) |

### Odds Data

Downloaded from [football-data.co.uk](https://www.football-data.co.uk/englandm.php).

Seasons: 2016-17 to 2023-24. Download the CSV for each season and save as `odds_raw_{season}.csv`.

| File | Description |
|---|---|
| `odds_clean.csv` | Cleaned odds with consistent column mapping |

### Generated Files (by notebook)

| File | Notebook | Description |
|---|---|---|
| `ou_parameters.csv` | 02 | O-U params per team-season |
| `eligible_teams.csv` | 02 | 20 teams passing stationarity filter |
| `pooled_adf_results.csv` | 02 | ADF test results |
| `pl_kalman_strength.csv` | 03 | Match-level Kalman estimates |
| `kalman_end_season.csv` | 03 | End-of-season strength rankings |
| `pl_hmm_regimes.csv` | 04 | Match-level regime labels |
| `hmm_parameters.csv` | 04 | HMM state parameters per team |
| `hmm_validation.csv` | 04 | Regime validation against known events |
| `signals.csv` | 05A | 5068 signal observations with reversion |
| `bucket_stats.csv` | 05A | Reversion accuracy by z-score bucket |
| `bets_tradeable.csv` | 05B | 323 tradeable signals with odds |
| `sim_1x2_kelly.csv` | 05B | Kelly simulation results — 1X2 |
| `sim_ah_kelly.csv` | 05B | Kelly simulation results — AH |
| `sim_1x2_flat.csv` | 05B | Flat stake simulation — 1X2 |
| `sim_ah_flat.csv` | 05B | Flat stake simulation — AH |

## Environment

```bash
conda create -n xg_env python=3.11
conda activate xg_env
pip install understat aiohttp pandas numpy scipy statsmodels hmmlearn matplotlib requests
```

All data is stored as CSV — no parquet or pickle dependencies.
