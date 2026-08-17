# 📊 Credit Risk Analysis: Predictive Modeling & BI Dashboard

---

## 🎯 Project Overview

This repository contains an end-to-end data science project focused on predicting credit loan defaults. By leveraging machine learning classification algorithms and interactive business intelligence tools, this project aims to identify high-risk customers and uncover the driving factors behind loan defaults.

## 📁 Repository Architecture

```text
Credit-Risk-Analysis-Project/
│
├── notebooks/
│   └── credit_risk_nb.ipynb           # Main notebook containing EDA, feature engineering, and modeling[cite: 1]
│
├── datasets/
│   ├── raw_credit_risk_dataset.csv    # Raw dataset sourced from Kaggle[cite: 1]
│   └── processed_dataset.csv          # Cleaned dataset with engineered features ready for training[cite: 1]
│
├── dashboards/
│   └── Credit Risk Dashboard.pbix     # Interactive Power BI dashboard for visual analytics[cite: 1]
│
└── README.md                          # Project documentation[cite: 1]

```

---

## 📦 Technology Stack & Libraries

| Library | Version | Purpose |
| --- | --- | --- |
| `numpy` | ≥1.24 | Numerical computing and array manipulation

 |
| `pandas` | ≥2.0 | Data ingestion, cleaning, and aggregation

 |
| `matplotlib` | ≥3.7 | Fundamental data visualization (scatter plots, histograms)

 |
| `seaborn` | ≥0.12 | Advanced statistical visualizations (correlation heatmaps, bar plots)

 |
| `scikit-learn` | ≥1.3 | Machine learning pipeline implementation, specifically Logistic Regression

 |

**Installation:**

```bash
pip install numpy pandas matplotlib seaborn scikit-learn

```

---

## 🗂️ Dataset Information

| Field | Details |
| --- | --- |
| **Dataset Name** | Credit Risk Dataset

 |
| **Source** | [Kaggle — laotse/credit-risk-dataset](https://www.kaggle.com/datasets/laotse/credit-risk-dataset)<br> |
| **License** | CC0: Public Domain

 |
| **Volume** | 32,574 records (post-cleaning)

 |
| **Target Variable** | `loan_status` (0 = Good Credit, 1 = Default)

 |

---

## 🚀 Getting Started

To replicate this analysis on your local machine, follow these steps:

1. **Clone the repository:**
```bash
git clone https://github.com/isasebib/credit-risk-analysis.git
cd credit-risk-analysis

```


2. **Install the required dependencies:**
```bash
pip install numpy pandas matplotlib seaborn scikit-learn

```


3. **Download the dataset:**
* Download the `credit_risk_dataset.csv` file from [Kaggle](https://www.kaggle.com/datasets/laotse/credit-risk-dataset).


* Ensure the file path in the `pd.read_csv()` function within the notebook points to your downloaded file.




4. **Launch Jupyter Notebook:**
```bash
jupyter notebook Credit-risk.ipynb

```


5. **Execute the code:** Run all cells sequentially via **Kernel → Restart & Run All**.



---

## 🔬 Core Research Questions

This analysis was designed to answer the following business-critical questions:

1. How does the length of a customer's credit history impact their likelihood of default?


2. Which loan purposes carry the highest risk of default, and does this align with the assigned interest rates?


3. Among the engineered features—employment stability, loan-to-income ratio, and loan burden index—which serves as the strongest predictor of default?



---

## 📈 Model Performance & Evaluation

The Logistic Regression model was evaluated using standard classification metrics:

| Metric | Score |
| --- | --- |
| **Accuracy** | 83.61%

 |
| **ROC-AUC Score** | 0.8323

 |
| **Recall (Default Sensitivity)** | 41%

 |

---

## 📊 Business Intelligence — Power BI Dashboard

To facilitate executive reporting and data exploration, a supplementary interactive dashboard was developed.

| Field | Details |
| --- | --- |
| **File Location** | `dashboard/Credit_Risk_Dashboard.pbix`<br> |
| **Platform** | Microsoft Power BI Desktop

 |
| **Contents** | Visualizes the distribution of credit risk, customer segmentation, and key risk metrics.

 |

> ⚠️ **Note:** To view and interact with the dashboard, you must have [Power BI Desktop](https://powerbi.microsoft.com/desktop/) installed (available for free).
> 
> 
