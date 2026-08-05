# 🌫️ Air Quality Classification in DKI Jakarta using Random Forest

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10-blue?logo=python">
  <img src="https://img.shields.io/badge/Scikit--Learn-Random%20Forest-orange?logo=scikitlearn">
  <img src="https://img.shields.io/badge/Google-Colab-F9AB00?logo=googlecolab">
  <img src="https://img.shields.io/badge/Status-Completed-success">
  <img src="https://img.shields.io/badge/License-MIT-green">
</p>

---

## 📌 Project Overview

This project aims to classify **Jakarta Air Quality (ISPU)** into four categories using a **Random Forest Classifier**.

The model predicts air quality based on pollutant concentrations measured from five monitoring stations across DKI Jakarta.

The project focuses not only on achieving high accuracy but also on implementing proper Machine Learning practices such as:

- Preventing Data Leakage
- Handling Imbalanced Dataset
- Robust Data Preprocessing
- Model Evaluation using multiple metrics
- Feature Importance Analysis

---

# 📚 Table of Contents

- Project Overview
- Dataset
- Objectives
- Tech Stack
- Workflow
- Repository Structure
- Results
- Key Findings
- How to Run
- Author

---

# 📊 Dataset

**Source**

https://www.kaggle.com/datasets/senadu34/air-quality-index-in-jakarta-2010-2021

Dataset contains daily ISPU observations from **2010–2021** collected by five monitoring stations in Jakarta.

Main pollutant variables:

- PM10
- SO₂
- CO
- O₃
- NO₂

Target variable:

- BAIK
- SEDANG
- TIDAK SEHAT
- SANGAT TIDAK SEHAT

---

# 🎯 Objectives

The objectives of this project are:

- Build a multiclass classification model using Random Forest.
- Prevent data leakage during preprocessing.
- Handle highly imbalanced classes.
- Evaluate model robustness using Macro F1-Score.
- Identify the most influential pollutants affecting air quality.

---

# 🛠 Tech Stack

| Category | Tools |
|-----------|--------|
| Language | Python |
| Notebook | Google Colab |
| ML Library | Scikit-Learn |
| Data Processing | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Model | Random Forest |
| Serialization | Pickle |

---

# 🔄 Machine Learning Pipeline

```
Raw Dataset
      │
      ▼
Exploratory Data Analysis
      │
      ▼
Data Cleaning
      │
      ▼
Feature Engineering
      │
      ▼
Train/Test Split
      │
      ▼
Random Forest Training
      │
      ▼
Model Evaluation
      │
      ▼
Feature Importance
```

---

# ⚙️ Preprocessing

The preprocessing pipeline includes:

✔ Removing data leakage columns (`max`, `critical`)

✔ Handling missing values using Median Imputation

✔ Removing PM2.5 (100% missing)

✔ Outlier treatment using IQR Capping

✔ Scaling features using RobustScaler

✔ Exporting processed dataset into Pickle format

---

# 🤖 Model

Algorithm used:

**Random Forest Classifier**

Configuration:

- class_weight = balanced
- Stratified Train-Test Split
- Smart handling for extremely rare classes

---

# 📈 Evaluation Metrics

Model performance is evaluated using:

- Accuracy
- Precision
- Recall
- Macro F1 Score
- ROC AUC (OvR)
- Confusion Matrix
- Feature Importance

---

# 📁 Repository Structure

```
.
├── data/
│   └── ispu_dki_all.csv
│
├── notebooks/
│   ├── 1_EDA.ipynb
│   ├── 2_Preprocessing.ipynb
│   ├── 3_Modeling.ipynb
│   └── 4_Evaluation.ipynb
│
├── pkl_files/
│   ├── data_preprocessed.pkl
│   └── model_bundle.pkl
│
├── images/
│
├── requirements.txt
└── README.md
```

---

# 📊 Results

## Model Performance

| Metric | Score |
|---------|-------|
| Accuracy | XX% |
| Precision | XX% |
| Recall | XX% |
| Macro F1 Score | XX% |

---

## Confusion Matrix

![](images/confusion_matrix.png)

---

## Classification Report

![](images/classification_report.png)

---

## ROC Curve

![](images/roc_auc.png)

---

## Feature Importance

![](images/feature_importance.png)

---

# 💡 Key Findings

- Random Forest successfully classified Jakarta air quality with very high performance.
- Proper preprocessing significantly improved model robustness.
- Removing data leakage columns prevented unrealistic accuracy.
- O₃ and PM10 were among the most influential pollutants.
- Macro F1 Score provided better evaluation than Accuracy due to class imbalance.

---

# 🚀 How to Run

Clone this repository

```bash
git clone https://github.com/dhafamarcelio/data-mining-ispu-dki-jakarta.git
```

Install dependencies

```bash
pip install -r requirements.txt
```

Run notebooks sequentially:

```
1_ispu_eda.ipynb
↓
2_ispu_preprocessed.ipynb
↓
3_ispu_modeling.ipynb
↓
4_ispu_evaluation.ipynb
```

---

# 🔮 Future Improvements

- Hyperparameter tuning using GridSearchCV
- Compare with XGBoost
- Deploy model using Streamlit
- Real-time prediction using Jakarta Open Data API

---

# 👨‍💻 Author

**Dhafa Marcelio**

Instagram

https://instagram.com/dapdhapa

Facebook

https://facebook.com/muhammad.dhafa.3720190

---

## ⭐ Support

If you find this project useful, don't forget to give this repository a **Star ⭐**.

---

## 📄 License

This project is licensed under the MIT License.