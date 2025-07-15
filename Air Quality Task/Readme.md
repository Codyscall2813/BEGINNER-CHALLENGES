**Air Quality Prediction and Forecasting System**

---

## 🚀 Project Overview

Air quality is a critical environmental and public health indicator. This project analyzes air quality data from 26 Indian cities (January 2021 – December 2022) to:

* **Preprocess** and clean raw pollutant measurements (e.g., CO, NO₂, PM₂.₅).
* **Engineer features** and prepare both tabular and time-series datasets.
* Build and evaluate two forecasting models:

  1. **Prophet** (Facebook-developed time-series model)
  2. **LSTM** (Long Short-Term Memory neural network)
* **Compare** model performance and select the best for accurate short-term air quality forecasts.

---

## 📁 Repository Structure

```
├── data/                       # Raw and processed CSV files
│   ├── air_quality_raw.csv     # Original measurements
│   ├── air_quality_preprocessed.csv
│   ├── air_quality_features.csv
│   └── future_predictions_7_days.csv
│
├── notebooks/                  # Jupyter notebooks
│   ├── data_preprocessing.ipynb
│   ├── feature_engineering.ipynb
│   ├── prophet_model.ipynb
│   └── lstm_model.ipynb
│
├── models/                     # Trained model artifacts
│   ├── prophet_model.pkl
│   └── lstm_air_quality_model.h5
│
├── outputs/                    # Exported results and metrics
│   ├── air_quality_predictions_complete.csv
│   └── model_comparison_metrics.csv
│
├── requirements.txt            # Python dependencies
├── environment.yml             # Conda environment file (optional)
├── train.py                    # Script to run full pipeline end-to-end
└── README.md                   # Project overview and instructions
```

---

## 🛠️ Installation & Setup

1. **Clone the repository**:

   ```bash
   git clone https://github.com/username/air-quality-forecast.git
   cd air-quality-forecast
   ```

2. **Install dependencies**:

   ```bash
   pip install -r requirements.txt
   # or using Conda
   conda env create -f environment.yml
   conda activate air-quality
   ```

3. **Run the full pipeline**:

   ```bash
   python train.py
   ```

---

## 🧹 Data Preprocessing

* **Dataset shape**: 23,504 records × 11 features
* **Cities covered**: 26
* **Date range**: 2020-11-30 – 2023-05-25

1. **Invalid value handling**: Replaced sentinel `-200` values with `NaN` (none found).
2. **Datetime conversion**: Transformed `DD-MM-YYYY` strings to `YYYY-MM-DD HH:MM:SS` and sorted chronologically.
3. **Final shape**: 23,504 rows × 12 columns (date column as datetime).

---

## ✨ Feature Engineering

* **Target variable**: `pm2_5`
* **Features**: `['co', 'no', 'no2', 'o3', 'so2', 'pm10', 'nh3', 'aqi']`
* **Scaling**: StandardScaler (zero mean, unit variance)
* **Time-series aggregation**: Daily national average PM₂.₅ for Prophet (`904` days)

---

## 🤖 Model Development & Evaluation

### 1. Time-Series Model: Prophet

* **Train/Test split**: 723 days (train), 181 days (test)
* **Metrics (test)**:

  * MAE: 22.24 μg/m³
  * RMSE: 28.36 μg/m³
  * R²: 0.7016 (Good performance)

### 2. Deep Learning Model: LSTM

* **Sequence length**: 30 days
* **Train/Test split**: 693 sequences (train), 181 sequences (test)
* **Architecture**: Two stacked LSTM layers + Dense output
* **Metrics (test)**:

  * MAE: 20.70 μg/m³
  * RMSE: 27.24 μg/m³
  * R²: 0.7247

### 📊 Model Comparison

| Model   | MAE (μg/m³) | RMSE (μg/m³) | R² Score |
| ------- | ----------: | -----------: | -------: |
| Prophet |       22.24 |        28.36 |    0.702 |
| LSTM    |       20.70 |        27.24 |    0.725 |

**LSTM improved** over Prophet by:

* MAE: +6.9%
* RMSE: +4.0%
* R²: +3.3%

**Selected best model**: **LSTM**

---

## 🌤️ Future Predictions

* **Next 7 days forecast** of average PM₂.₅ levels:

  | Date       | PM₂.₅ (μg/m³) | Air Quality Category       |
  | ---------- | ------------: | -------------------------- |
  | 2023-05-24 |          60.5 | 🟠 Unhealthy for Sensitive |
  | 2023-05-25 |          62.4 | 🟠 Unhealthy for Sensitive |
  | 2023-05-26 |          64.5 | 🟠 Unhealthy for Sensitive |
  | 2023-05-27 |          60.9 | 🟠 Unhealthy for Sensitive |
  | 2023-05-28 |          46.2 | 🟡 Moderate                |
  | 2023-05-29 |          45.6 | 🟡 Moderate                |
  | 2023-05-30 |          62.4 | 🟠 Unhealthy for Sensitive |

*Confidence intervals included in outputs.*

---

## 📈 Visualizations

> *Add your plots and figures here.*

* ![Pollutant Trends](notebooks/figures/pollutant_trends.png)
* ![Feature Correlation](notebooks/figures/correlation_matrix.png)
* ![Prophet Forecast vs Actual](notebooks/figures/prophet_forecast.png)
* ![LSTM Loss Curves](notebooks/figures/lstm_train_val_loss.png)

---

## 💾 Output Files

* `air_quality_predictions_complete.csv`
* `future_predictions_7_days.csv`
* `model_comparison_metrics.csv`
* `lstm_air_quality_model.h5`
