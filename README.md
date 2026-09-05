# Freight Rate Prediction

XGBoost-based freight rate prediction model with Optuna hyperparameter tuning and Exponential Smoothing for December market index forecasting.

---

## Download the Project

Download the repository as a ZIP file from GitHub and extract it to a local folder.

Alternatively, you may clone the repository:

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

## Select the Jupyter Kernel

After installing the dependencies, open `solution.ipynb` and select the Python interpreter associated with the virtual environment.

### Windows

```text
.venv\Scripts\python.exe
```

### macOS / Linux

```text
.venv/bin/python
```

### VS Code

1. Open `solution.ipynb`.
2. Click **Select Kernel** in the upper-right corner.
3. Choose the interpreter from the `.venv` environment.

If the kernel is not available, run:

```bash
pip install ipykernel
python -m ipykernel install --user --name freight-rate-prediction
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
