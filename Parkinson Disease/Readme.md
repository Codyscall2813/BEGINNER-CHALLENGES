# Parkinson's Disease Prediction Using Machine Learning

> A comprehensive machine learning pipeline to predict Parkinson's disease from voice analysis features.

---

## 📋 Table of Contents

1. [Project Overview](#project-overview)
2. [Features](#features)
3. [Dataset](#dataset)
4. [Installation](#installation)
5. [Usage](#usage)
6. [Pipeline Steps](#pipeline-steps)

   * [1. Data Loading & Exploration](#1-data-loading--exploration)
   * [2. Data Preprocessing](#2-data-preprocessing)
   * [3. Exploratory Data Analysis](#3-exploratory-data-analysis)
   * [4. Model Training & Selection](#4-model-training--selection)
   * [5. Model Evaluation & Comparison](#5-model-evaluation--comparison)
   * [6. Hyperparameter Tuning](#6-hyperparameter-tuning)
   * [7. Final Predictions & Insights](#7-final-predictions--insights)
7. [Key Insights](#key-insights)
8. [Medical Significance](#medical-significance)
9. [Future Improvements](#future-improvements)
10. [Contributing](#contributing)
11. [License](#license)

---

## 📝 Project Overview

This repository implements a robust machine learning workflow to predict Parkinson's disease based on voice feature sets. By analyzing non-invasive voice recordings, the model assists in early screening and complements clinical diagnoses.

---

## ⭐ Features

* Data loading, exploration, and cleaning
* Handling class imbalance with SMOTE
* Feature scaling and selection
* Comparative training of multiple algorithms (Logistic Regression, Random Forest, SVM, XGBoost)
* Cross-validation and hyperparameter tuning
* Detailed model evaluation and visualization

---

## 📂 Dataset

* **Source**: \[Link to dataset source if applicable]
* **Samples**: 756
* **Features**: 754 voice-based attributes
* **Classes**: 2 (Healthy = 0, Parkinson's = 1)

```text
Dataset shape: (756, 755)
Missing values: 0
Duplicate rows: 1
Class distribution: Healthy (0): 192 (25.4%), Parkinson's (1): 564 (74.6%)
```

---

## ⚙️ Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/username/parkinson-prediction.git
   cd parkinson-prediction
   ```
2. Create and activate a virtual environment:

   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```
3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

---

## 🚀 Usage

Run the main pipeline script with:

```bash
python main.py --config config.yaml
```

Customize hyperparameters and paths in `config.yaml`.

---

## 🔄 Pipeline Steps

### 1. Data Loading & Exploration

```text
Dataset shape: (756, 755)
Number of features: 754
Number of samples: 756
Dataset Info: Missing values: 0, Duplicate rows: 1
Class Distribution: Healthy (0): 192 (25.4%), Parkinson's (1): 564 (74.6%)
```

### 2. Data Preprocessing

```text
Features shape: (756, 753)
Target shape: (756,)
Class imbalance ratio: 0.746
⚠️  Class imbalance detected! Applying SMOTE...
After SMOTE - Features shape: (1128, 753)
After SMOTE - Class distribution: [564 564]
Training set shape: (902, 753)
Test set shape: (226, 753)
```

### 3. Exploratory Data Analysis

Top 10 Feature Correlations with Target:

```text
mean_MFCC_2nd_coef         0.398695
... (see full list in notebook)
std_9th_delta_delta        0.364333
```

### 4. Model Training & Selection

Training and comparing four models:

* **Logistic Regression**: Accuracy 0.938 | ROC-AUC 0.967 | CV Score 0.912 (±0.044)
* **Random Forest**: Accuracy 0.929 | ROC-AUC 0.991 | CV Score 0.918 (±0.058)
* **SVM**: Accuracy 0.942 | ROC-AUC 0.990 | CV Score 0.911 (±0.018)
* **XGBoost**: Accuracy 0.956 | ROC-AUC 0.995 | CV Score 0.946 (±0.018)

### 5. Model Evaluation & Comparison

```text
Model Performance Comparison:
                     accuracy  precision  recall  f1_score  roc_auc  cv_mean  cv_std
XGBoost                 0.956      0.972   0.938     0.955    0.995   0.946  0.009
...
🎯 Best Model: XGBoost (ROC-AUC 0.995)
```

Detailed XGBoost Classification Report:

```text
              precision    recall  f1-score   support
Healthy       0.94      0.97      0.96       113
Parkinson's   0.97      0.94      0.95       113
```

Top 10 Most Important Features:

```text
440  tqwt_TKEO_mean_dec_12    0.082242
... (full list available in notebook)
```

### 6. Hyperparameter Tuning

```text
Best parameters: {'learning_rate': 0.2, 'max_depth': 5, 'n_estimators': 200}
Best CV score: 0.982
```

### 7. Final Predictions & Insights

```text
Sample Predictions:
Actual  Predicted  Probability
908       0          0     0.000597
... (ten examples)
```

Final Model Performance:

```text
Model: XGBoost
Accuracy: 0.960 (96.0%)
ROC-AUC: 0.997 (99.7%)

✅ Model and scaler saved successfully!
```

---

## 📊 Key Insights

1. Class imbalance handled effectively using SMOTE.
2. Feature scaling boosted model performance.
3. XGBoost outperforms other classical methods on voice data.
4. Acoustic features (PPE, DFA, RPDE) are strong predictors.
5. Achieves high accuracy suitable for clinical screening.

---

## 🔬 Medical Significance

* Enables early, non-invasive Parkinson's screening via voice analysis.
* Complements clinical diagnostics for timely intervention.

---

## 🛠 Future Improvements

* Gather larger, balanced datasets.
* Explore deep learning architectures (CNNs, RNNs).
* Implement ensemble stacking for further gains.
* Validate models on external cohorts.
* Develop real-time voice analysis application.

---

## 🤝 Contributing

Contributions are welcome! Please open issues or submit pull requests.
