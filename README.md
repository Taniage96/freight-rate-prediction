# Freight Rate Prediction

XGBoost model for predicting freight load rates, with Optuna hyperparameter tuning and Exponential Smoothing for December market index forecasting.

## Setup

```bash
python -m venv .venv
.venv\Scripts\activate        # Windows
pip install -r requirements.txt
```

## Run

Open `solution.ipynb` in VS Code or Jupyter and run all cells in order.

The notebook produces:
- `outputs/validation_predictions.csv` — 12,000 rate predictions
- `outputs/december-chart-inputs.csv` — 31 daily December forecasts (Lexington → Fort Wayne)

## Validate outputs

```bash
python score.py \
  --predictions outputs/validation_predictions.csv \
  --december-predictions outputs/december-chart-inputs.csv
```

This validates both files and generates `outputs/scorer_results/candidate_december.png`.

## Approach

| Step | Detail |
|---|---|
| Split | Temporal — last month of training data as hold-out |
| Target | log(posted_rate + 1) — reduces right skew |
| Features | 30 features: route-level rate/mile stats, haversine distance, sinuosity, geographic region grid |
| Model | XGBoost with 75-trial Optuna search (TPE sampler) |
| December indices | Exponential Smoothing (trend + weekly seasonality) on historical market_index/quote_signal |

## Results (hold-out — October 2025)

| Metric | Baseline (Ridge) | XGBoost + Optuna |
|---|---|---|
| RMSE | $733 | $640 |
| MAE | $221 | $112 |
| Median AE | — | $32 |
| WMAPE | 9.3% | 4.7% |
| R² | 0.77 | 0.83 |

The RMSE gap vs MAE is driven by 63 loads (1.3%) with anomalous rate-per-mile values (4–6× the route average), likely reflecting spot market surges or backhaul imbalances not captured by available features.
