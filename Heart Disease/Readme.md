# Heart Disease Prediction System

> A comprehensive machine learning pipeline for predicting 10-year risk of coronary heart disease using Framingham Heart Study data.

---

## 🚀 Table of Contents

1. [Project Overview](#project-overview)
2. [Dataset](#dataset)
3. [Installation](#installation)
4. [Usage](#usage)
5. [Project Structure](#project-structure)
6. [Methodology](#methodology)

   * [Data Loading & Preprocessing](#data-loading--preprocessing)
   * [Exploratory Data Analysis](#exploratory-data-analysis)
   * [Feature Engineering & Scaling](#feature-engineering--scaling)
   * [Modeling Approaches](#modeling-approaches)
7. [Results & Evaluation](#results--evaluation)

   * [Original Logistic Regression](#original-logistic-regression)
   * [Class Balancing Techniques](#class-balancing-techniques)
   * [Random Forest & Threshold Optimization](#random-forest--threshold-optimization)
   * [Model Comparison](#model-comparison)
8. [Visualizations](#visualizations)
9. [Prediction Example](#prediction-example)
10. [Clinical Insights & Recommendations](#clinical-insights--recommendations)
11. [Future Work](#future-work)
12. [License](#license)
13. [Acknowledgements](#acknowledgements)

---

## Project Overview

The goal of this project is to develop and evaluate machine learning models to predict the 10-year risk of coronary heart disease (CHD) using logistic regression and other algorithms, addressing class imbalance to improve recall on the minority CHD-positive class.

Key achievements:

* **Data preprocessing** and handling of missing values from 4,240 samples to 3,751 clean records.
* Baseline **Logistic Regression** with accuracy 84.90% and ROC-AUC 0.7360.
* Enhanced models using **class weights**, **SMOTE**, **Random Forest**, and **threshold optimization**.
* Improved recall from 4.1% to 66.9% (LR + SMOTE) and F1-score from 7.6% to 41.1%.

---

## Dataset

* **Source:** Framingham Heart Study dataset
* **Samples:** 4,240 participants
* **Features:** 16 original variables (gender, age, smoking status, blood pressure, cholesterol, BMI, glucose, etc.)
* **Target:** `TenYearCHD` (binary: 1 = CHD within 10 years, 0 = no CHD)
* **Cleaned samples:** 3,751 after removing missing values (\~11.5% removed)

See [data/raw/framingham.csv](data/raw/framingham.csv) for the original file.

---

## Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/username/heart-disease-prediction.git
   cd heart-disease-prediction
   ```
2. Create a Python environment and install dependencies:

   ```bash
   python3 -m venv venv
   source venv/bin/activate    # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

---

## Usage

1. **Data Preprocessing & EDA**

   ```bash
   python src/01_data_preprocessing.py
   python src/02_exploratory_analysis.py
   ```
2. **Model Training & Evaluation**

   ```bash
   python src/03_model_training.py        # Logistic Regression, class balancing, SMOTE
   python src/04_random_forest.py        # Random Forest with class weights
   python src/05_threshold_optimization.py
   ```
3. **Generate Visualizations**

   ```bash
   python src/06_visualizations.py
   ```
4. **Predict on New Data**

   ```bash
   python src/predict.py --input examples/new_patient.json
   ```

---

## Project Structure

```
├── data
│   ├── raw
│   │   └── framingham.csv
│   └── processed
│       └── framingham_clean.csv
├── src
│   ├── 01_data_preprocessing.py
│   ├── 02_exploratory_analysis.py
│   ├── 03_model_training.py
│   ├── 04_random_forest.py
│   ├── 05_threshold_optimization.py
│   ├── 06_visualizations.py
│   └── predict.py
├── models
│   ├── log_reg_original.pkl
│   ├── log_reg_smote.pkl
│   ├── rf_balanced.pkl
│   └── scaler.pkl
├── examples
│   └── new_patient.json
├── notebooks
│   └── heart_disease_analysis.ipynb
├── requirements.txt
└── README.md
```

---

## Methodology

### Data Loading & Preprocessing

* Load raw CSV and inspect shape `(4240, 16)`.
* Analyze missing values, drop `education` column, and remove rows with missing entries, resulting in 3,751 records.
* Rename columns for clarity.

### Exploratory Data Analysis

* Visualize target distribution: 84.8% no-CHD vs. 15.2% CHD.
* Compare means of key variables (age, cholesterol, systolic BP, BMI, glucose) by CHD status.

### Feature Engineering & Scaling

* Selected 14 features, split into train (70%) and test (30%) sets.
* Normalize features using `StandardScaler`.

### Modeling Approaches

1. **Original Logistic Regression:** Baseline model
2. **Balanced Logistic Regression:** Class weights inverse to frequency
3. **SMOTE + Logistic Regression:** Oversample minority class
4. **Random Forest:** Class-weighted ensemble
5. **Threshold Optimization:** Adjust probability cutoff for best F1-score

---

## Results & Evaluation

### Original Logistic Regression

* **Accuracy:** 84.90%
* **Precision (CHD):** 58.33%
* **Recall (CHD):** 4.07%
* **F1-Score:** 7.61%
* **ROC-AUC:** 0.7360

### Class Balancing Techniques

* **Balanced LR:** Recall ↑ to 65.12%, F1 ↑ to 37.90% (Accuracy drops to 67.41%)
* **LR + SMOTE:** Recall 66.86%, F1 38.72%, similar ROC-AUC 0.7307

### Random Forest & Threshold Optimization

* **Random Forest:** ROC-AUC 0.6855, moderate recall
* **Optimal Threshold (LR):** F1 41.10%, recall 56.40%, ROC-AUC 0.7340

### Model Comparison

| Model                | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
| -------------------- | -------- | --------- | ------ | -------- | ------- |
| Original LR          | 0.8490   | 0.5833    | 0.0407 | 0.0761   | 0.7360  |
| Balanced LR          | 0.6741   | 0.2673    | 0.6512 | 0.3790   | 0.7340  |
| LR + SMOTE           | 0.6767   | 0.2725    | 0.6686 | 0.3872   | 0.7307  |
| Random Forest        | 0.8144   | 0.3271    | 0.2035 | 0.2509   | 0.6855  |
| Optimal Threshold LR | 0.7531   | 0.3233    | 0.5640 | 0.4110   | 0.7340  |

---

## Visualizations

> **Insert your EDA and model performance plots here**:
>
> * Distribution of CHD vs. no-CHD
> * Feature importance bar charts
> * ROC curves

![EDA\_placeholder](docs/images/eda_placeholder.png)

---

## Prediction Example

```json
# Input (new_patient.json)
{
  "gender_male": 1,
  "age": 65,
  "current_smoker": 1,
  "cigarettes_per_day": 25,
  "bp_medications": 1,
  "prevalent_stroke": 0,
  "prevalent_hypertension": 1,
  "diabetes": 1,
  "total_cholesterol": 280,
  "systolic_bp": 160,
  "diastolic_bp": 95,
  "bmi": 30.5,
  "heart_rate": 85,
  "glucose": 120
}
```

**Output:**

```
10-Year CHD Risk Probability: 92.18% → HIGH RISK ⚠️
Recommendation: Immediate cardiology consultation.
```

---

## Clinical Insights & Recommendations

* **Key Risk Factors:** Age, systolic blood pressure, total cholesterol, BMI, glucose.
* **Clinical Use:** Best used as a screening tool, not a diagnostic replacement.
* **Deployment:** Retraining on new data, threshold tuning based on clinical cost of false negatives.

---

## Future Work

* Ensemble methods (XGBoost, neural networks)
* Incorporate additional features (family history, genetic markers)
* External validation on diverse cohorts
* Integration with electronic health record (EHR) systems

---

## Acknowledgements

* Framingham Heart Study contributors
* Open-source libraries: scikit-learn, imbalanced-learn, pandas, matplotlib
* Inspired by clinical data science best practices
