# 🏠 House Price Predictor

> A end-to-end machine learning pipeline to predict residential property prices — from raw data to a deployable REST API.

[![CI](https://github.com/LeVraiToT/house-price-predictor/actions/workflows/ci.yml/badge.svg)](https://github.com/LeVraiToT/house-price-predictor/actions)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📌 Overview

This project builds a supervised regression model to predict house prices based on structural and location features. It covers the full ML lifecycle:

- **Data ingestion & cleaning** — automated preprocessing pipeline
- **Exploratory Data Analysis** — feature distributions, correlations, outlier detection
- **Feature engineering** — encoding, scaling, interaction terms
- **Model training & tracking** — scikit-learn models tracked with MLflow
- **REST API** — predictions served via FastAPI
- **CI/CD** — automated linting and tests with GitHub Actions

**Dataset**: [Kaggle House Prices](https://www.kaggle.com/c/house-prices-advanced-regression-techniques) (or California Housing via `sklearn.datasets`)

---

## 🗂️ Project Structure

```
house-price-predictor/
├── data/
│   ├── raw/                  # Original, immutable data
│   └── processed/            # Cleaned and feature-engineered data
├── notebooks/
│   ├── 01_eda.ipynb          # Exploratory Data Analysis
│   ├── 02_feature_eng.ipynb  # Feature engineering experiments
│   └── 03_modeling.ipynb     # Model comparison and selection
├── src/
│   ├── data_preprocessing.py # Cleaning and transformation pipeline
│   ├── train.py              # Model training entry point
│   └── predict.py            # Inference utilities
├── tests/
│   └── test_preprocessing.py # Unit tests (pytest)
├── app/
│   └── main.py               # FastAPI application
├── .github/
│   └── workflows/
│       └── ci.yml            # GitHub Actions CI pipeline
├── requirements.txt
├── .gitignore
├── MLproject                 # MLflow project config
└── README.md
```

---

## ⚡ Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/LeVraiToT/house-price-predictor.git
cd house-price-predictor
```

### 2. Create and activate a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate       # Linux/macOS
.venv\Scripts\activate          # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the preprocessing pipeline

```bash
python src/data_preprocessing.py --input data/raw/train.csv --output data/processed/
```

### 5. Train a model

```bash
python src/train.py --model ridge --experiment house_prices
```

### 6. Launch the API locally

```bash
uvicorn app.main:app --reload
# → http://localhost:8000/docs
```

---

## 🧪 Running Tests

```bash
pytest tests/ -v
```

---

## 📊 MLflow Experiment Tracking

All training runs are tracked with MLflow (parameters, metrics, artifacts).

```bash
mlflow ui
# → http://localhost:5000
```

Key tracked metrics:
- `RMSE` — Root Mean Squared Error
- `MAE` — Mean Absolute Error
- `R²` — Coefficient of determination

---

## 🔌 API Reference

Once the server is running, the interactive docs are available at `http://localhost:8000/docs`.

### `POST /predict`

```json
{
  "GrLivArea": 1500,
  "OverallQual": 7,
  "YearBuilt": 2003,
  "TotalBsmtSF": 856,
  "GarageArea": 548
}
```

**Response:**

```json
{
  "predicted_price": 213500.0,
  "model_version": "v1.0.0"
}
```

---

## 🌿 Git Workflow

This project follows a **feature branch workflow**:

```
main          ← stable, production-ready
└── dev       ← integration branch
    ├── feature/eda
    ├── feature/model-ridge
    └── feature/fastapi-endpoint
```

Commit convention: [Conventional Commits](https://www.conventionalcommits.org/)

```
feat: add ridge regression baseline
fix: handle missing values in GarageArea
docs: update API reference in README
test: add unit tests for preprocessing pipeline
```

---

## 📈 Results

| Model | RMSE | MAE | R² |
|-------|------|-----|----|
| Linear Regression (baseline) | 38,200 | 27,100 | 0.78 |
| Ridge Regression | 31,500 | 22,800 | 0.84 |
| Gradient Boosting | 24,800 | 17,300 | 0.91 |

*Results on the validation set (20% split).*

---

## 🛣️ Roadmap

- [x] EDA & feature engineering
- [x] Baseline model (Linear Regression)
- [x] Ridge and Gradient Boosting models
- [x] MLflow experiment tracking
- [x] FastAPI endpoint
- [ ] Dockerize the API
- [ ] Deploy to Render / Hugging Face Spaces
- [ ] Add SHAP feature importance

---

## 📄 License

MIT © [LeVraiToT](https://github.com/LeVraiToT)
