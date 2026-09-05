# Freight Rate Prediction

XGBoost-based freight rate prediction model with Optuna hyperparameter tuning and Exponential Smoothing for December market index forecasting.

---

## Clone Repository

```bash
git clone https://github.com/Taniage96/freight-rate-prediction.git
cd freight-rate-prediction
```

---

## Setup

### Windows

Create and activate a virtual environment:

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

### macOS / Linux

Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

---

## Run the Solution

Open `solution.ipynb` in VS Code or Jupyter Notebook and run all cells in order.

The notebook generates:

- `outputs/validation_predictions.csv` - Freight rate predictions for the 12,000 validation loads.
- `outputs/december-chart-inputs.csv` - December market index forecasts used by the scoring script.

---

## Validate Outputs

### Windows

```bash
python score.py --predictions outputs/validation_predictions.csv --december-predictions outputs/december-chart-inputs.csv
```

### macOS / Linux

```bash
python3 score.py --predictions outputs/validation_predictions.csv --december-predictions outputs/december-chart-inputs.csv
```

The scorer validates both output files and generates:

```text
scorer_results/candidate_december.png
```

---

## Project Structure

```text
.
├── solution.ipynb
├── score.py
├── requirements.txt
├── README.md
├── Final Report.pdf
├── train-test.csv
├── validation.csv
├── validation-predictions-template.csv
├── outputs/
│   ├── validation_predictions.csv
│   ├── december-chart-inputs.csv
│   └── *.png
└── scorer_results/
    └── c*ndidate_december.png
```

---

## *odeling Approach

| Step | Descrip*ion |
|--------|-------------|
| D*ta Split | Temporal split using th* last month of training data as a *old-out validation set |
| Target *ransformation | `log(posted_rate +*1)` to reduce right skewness |
| F*ature Engineering | Route-level ra*e-per-mile statistics, haversine d*stance, sinuosity, and geographic *egion features |
| Model | XGBoost*optimized using a 75-trial Optuna *earch (TPE sampler) |
| December F*recasting | Exponential Smoothing *ith trend and weekly seasonality |*
---

## Validation Results

| Met*ic | Baseline (Ridge) | XGBoost + *ptuna |
|----------|----------|---*------|
| RMSE | $733 | $640 |
| M*E | $221 | $112 |
| Median AE | — * $32 |
| WMAPE | 9.3% | 4.7% |
| R* | 0.77 | 0.83 |

The remaining RM*E gap relative to MAE is primarily*driven by a small set of outlier l*ads (approximately 1.3% of observa*ions) exhibiting rate-per-mile val*es 4 to 6 times higher than their *oute averages.

---

## Deliverabl*s

- Source code and modeling note*ook (`solution.ipynb`)
- `outputs/*alidation_predictions.csv`
- `Fina* Report.pdf`
- December forecast o*tputs and visualizations
- Loom pr*sentation (submitted separately)
`*
