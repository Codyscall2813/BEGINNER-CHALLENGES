# 🚀 Bitcoin Price Prediction System

Predict and analyze Bitcoin prices with robust data pipelines, classical and deep learning models, and a production-ready ensemble.

---

## 📋 Table of Contents

1. [Overview](#overview)
2. [Pipeline Summary](#pipeline-summary)
3. [Features](#features)
4. [Getting Started](#getting-started)

   * [Prerequisites](#prerequisites)
   * [Installation](#installation)
   * [Configuration](#configuration)
5. [Usage](#usage)

   * [Data Loading & Preprocessing](#data-loading--preprocessing)
   * [Technical Indicators](#technical-indicators)
   * [Feature Engineering](#feature-engineering)
   * [Exploratory Data Analysis](#exploratory-data-analysis)
   * [Model Training & Selection](#model-training--selection)
   * [Model Evaluation & Comparison](#model-evaluation--comparison)
6. [Project Structure](#project-structure)
7. [Key Results](#key-results)
8. [Future Enhancements](#future-enhancements)
9. [Contributing](#contributing)
10. [License](#license)
11. [Acknowledgements](#acknowledgements)

---

## Overview

This project implements a full Bitcoin price prediction pipeline:

* **Data Retrieval & Cleaning**: Load historical data (2014–2022) and ensure no missing values.
* **Indicator Engineering**: Create SMA, EMA, MACD, Bollinger Bands, RSI, volatility, and lag features.
* **Modeling**: Train linear, tree-based, SVM, XGBoost, LSTM, and linear ensemble models.
* **Evaluation**: Compare models via RMSE, MAE, and R²; select champions for production.
* **Production Pipeline**: Optimize features, train champion linear models (Lasso, Ridge, Linear), build ensemble for deployment.

## Pipeline Summary

```text
Dataset: 2713 records, 7 columns (2014-09-17 to 2022-02-19)
No missing values detected.

Technical Indicators: SMA, EMA, MACD, Bollinger Bands, RSI, volatility, momentum, lag features.
Features: 2682 samples, 25 engineered variables.

Models Trained:
 • Linear Regression (RMSE: $1,652.40)
 • Random Forest (RMSE: $28,085.74)
 • SVM (RMSE: $37,218.32)
 • XGBoost (RMSE: $29,896.32)
 • LSTM (RMSE: $6,518.24)

Champion Classical: Linear Regression (R²=0.989)
Champion Deep: LSTM (R²=0.819)

Production Models: Lasso, Linear, Ridge (R²≈0.978, RMSE≈$2,329)
Ensemble RMSE: $2,329, R²=0.978
```

## Features

* **Data Handling**: `pandas`, `numpy`
* **Visualizations**: `matplotlib`, `plotly`
* **Indicators**: SMA, EMA, MACD, Bollinger Bands, RSI, volatility, momentum, lag
* **Modeling**: `scikit-learn`, `XGBoost`, `TensorFlow/Keras`
* **API Access**: `ccxt` or REST for live data fetching
* **Evaluation**: RMSE, MAE, R²

## Getting Started

### Prerequisites

```bash
pip install pandas numpy matplotlib plotly ccxt prophet tensorflow scikit-learn xgboost
```

### Installation

1. Clone the repo:

   ```bash
   ```

git clone [https://github.com/your-username/bitcoin-prediction.git](https://github.com/your-username/bitcoin-prediction.git)
cd bitcoin-prediction

````
2. Install dependencies:
```bash
pip install -r requirements.txt
````

### Configuration

* If using exchange APIs, create `config.json` in the project root:

  ```json
  {
    "API_KEY": "YOUR_API_KEY",
    "API_SECRET": "YOUR_API_SECRET"
  }
  ```

## Usage

### Data Loading & Preprocessing

```bash
python src/data_pipeline.py --download --preprocess
```

* Loads 2713 rows; checks for missing values; outputs clean CSV.

### Technical Indicators

Generated indicators:

* Simple & Exponential MAs (7-day, 30-day, 12/26 EMA)
* MACD & Signal Line
* Bollinger Bands
* RSI
* Volatility & momentum metrics
* Lag features

### Feature Engineering

```bash
python src/feature_engineering.py --input data/clean.csv --output data/features.csv
```

* Creates 25-feature matrix (2682 samples).

### Exploratory Data Analysis

Review price stats and correlations:

* Min: \$178.10, Max: \$67,566.83, Mean: \$11,323.91, Volatility: 3.88%
* Top correlated features: Close (0.999), SMA\_7 (0.997), SMA\_30 (0.987)

### Model Training & Selection

```bash
python src/train_models.py --models all
```

* Trains Linear, RF, SVM, XGBoost, LSTM.

### Model Evaluation & Comparison

```bash
python src/evaluate.py --metrics rmse mae r2
```

* Linear Regression champion (RMSE: \$1,652, R²=0.989)
* LSTM deep champion (RMSE: \$6,518, R²=0.819)

## Project Structure

```text
bitcoin-prediction/
├── data/                     # Raw & processed data
│   ├── raw.csv
│   └── features.csv
├── src/                      # Source code modules
│   ├── data_pipeline.py      # Download & preprocess
│   ├── feature_engineering.py
│   ├── train_models.py       # Train classical & deep models
│   ├── evaluate.py           # Evaluation scripts
│   └── predict.py            # Production predictor interface
├── notebooks/
│   └── pybitcoin.ipynb       # EDA & prototyping notebook
├── reports/                  # Plots & reports (PNG, HTML)
├── requirements.txt
├── config.json (optional)    # API keys
└── README.md
```

## Key Results

| Model             |        RMSE |      MAE |     R² |
| ----------------- | ----------: | -------: | -----: |
| Linear Regression |  \$1,652.40 |  \$1,150 |  0.989 |
| LSTM              |  \$6,518.24 |  \$5,249 |  0.819 |
| Random Forest     | \$28,085.74 | \$24,046 | -2.191 |
| XGBoost           | \$29,896.32 | \$25,885 | -2.616 |
| SVM               | \$37,218.32 | \$32,598 | -4.603 |

**Production Ensemble (Lasso, Linear, Ridge)**:

* RMSE: \$2,329, R²=0.978

## Future Enhancements

1. Real-time data streaming from exchanges
2. Advanced feature selection and generation
3. Ensemble stacking and blending
4. Walk-forward cross-validation
5. API deployment as microservice
6. Real-time trading alerts and dashboard

## Contributing

Contributions are welcome! Please follow:

1. Fork repo & create branch (`git checkout -b feature/YourFeature`)
2. Commit & push changes
3. Open a Pull Request
