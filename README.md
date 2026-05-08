# ML-credit-card-default-classification
# Credit Card Default Prediction
### CSE374 — Machine Learning | Ain Shams University | May 2026

**Team:** Mena Moheb Abdelshaheed · George Ibrahim Abdo · Abdalla Ragaee Ahmed  
**Dataset Level:** 3 (+2 bonus) — UCI Credit Card Default (Taiwan)

---

## Problem
Predict whether a credit card client will default on their next payment.  
Binary classification: `1 = default`, `0 = no default`  
**30,000 clients · 23 original features · 6 months of payment history**

---

## Results Summary

| Model | Accuracy | Precision | Recall | F1 | AUC-ROC |
|---|---|---|---|---|---|
| Logistic Regression | 0.673 | 0.374 | 0.711 | 0.490 | 0.748 |
| **Decision Tree ✓** | **0.723** | **0.419** | **0.653** | **0.510** | **0.760** |
| kNN (k=15) | 0.599 | 0.326 | 0.761 | 0.456 | 0.729 |
| Neural Network (MLP) | 0.660 | 0.359 | 0.685 | 0.472 | 0.740 |

**Best model: Decision Tree (max_depth=5)** — highest F1 and AUC-ROC  
Decision threshold set to **0.40** (tuned on validation set, before touching test data)

---

## Pipeline Overview

1. **Data Cleaning** — fixed undocumented EDUCATION/MARRIAGE codes, winsorized outliers
2. **Feature Engineering** — 10 new behavioral features (max_delay, num_delays, payment_ratio, etc.)
3. **Preprocessing** — RobustScaler + SMOTE (training set only, no data leakage)
4. **Split** — 70% train · 10% validation · 20% test (stratified)
5. **Modeling** — 4 classifiers with hyperparameter tuning on validation set
6. **Evaluation** — F1, AUC-ROC, confusion matrices, ROC curves

├── CreditCardDefault.ipynb  # Full notebook (runs end-to-end)
├── Report.docx              # 10-page project report
├── Presentation.pptx                  # Defense slides
└── README.md



---

## How to Run

The notebook downloads the dataset automatically from UCI — no manual download needed.

```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn openpyxl
jupyter notebook CSE374_Milestone2_CreditCardDefault.ipynb
```

Run all cells top to bottom. Expected runtime: ~3–5 minutes.

---

## Dataset

**Source:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/default+of+credit+card+clients)  
Yeh, I.C. & Lien, C.H. (2009). *Expert Systems with Applications*, 36(2), 2473–2480.

---

## Key Engineering Decisions

- **SMOTE applied after splitting** — prevents data leakage into validation/test sets
- **RobustScaler over StandardScaler** — less sensitive to remaining skewness in financial data
- **Threshold = 0.40** — chosen to favor recall (missing a defaulter costs more than a false alarm)
- **Naive Bayes excluded** — correlated financial features violate independence assumption

---

*CSE374 Machine Learning · Faculty of Engineering · Ain Shams University*

---

## Repository Structure
