# 🧬 Cancer Risk Classification — End-to-End ML Pipeline

**Author:** [Tarek Masryo](https://www.kaggle.com/tarekmasryo)  
**License:** MIT (Code) · CC BY-NC 4.0 (Data)  

---

## 📘 Project Overview
A clean, reproducible machine learning pipeline for **cancer-type and risk-level prediction** from patient-level features.  
The notebook demonstrates how to **build, validate, and interpret** tabular healthcare models while avoiding **data leakage** — a common pitfall in clinical ML.

The goal is to show a **transparent, educational workflow**:  
data understanding → feature preprocessing → model benchmarking → interpretability.

---

## 🧩 Pipeline Summary

| Stage | Description |
|--------|--------------|
| **EDA & Validation** | Summary stats, missing-value checks, distribution plots, and correlation heatmaps |
| **Leakage Probe** | Confirms `Risk_Level` is derived from `Overall_Risk_Score`, which must be excluded during training |
| **Preprocessing** | Numeric imputation + scaling, categorical imputation + one-hot encoding via `ColumnTransformer` |
| **Model Comparison** | Cross-validated F1-macro scoring for Logistic Regression, Random Forest, Calibrated SVM, XGBoost, and Gradient Boosting |
| **Interpretability** | Confusion matrices + permutation importance showing which lifestyle or clinical features drive predictions |

---

## 📊 Dataset
**File:** `cancer-risk-factors.csv`  
**Rows:** ~1000 patients  
**Columns:** Demographics, lifestyle habits, genetic indicators, and risk scores  

| Feature | Description |
|----------|-------------|
| `Age`, `BMI` | Demographic metrics |
| `Smoking`, `Alcohol_Use`, `Obesity` | Lifestyle factors |
| `Family_History`, `BRCA_Mutation`, `H_Pylori_Infection` | Clinical/genetic indicators |
| `Overall_Risk_Score` | Numeric aggregation (excluded from training to avoid leakage) |
| `Risk_Level` | Derived categorical risk band (Low / Medium / High) |
| `Cancer_Type` | Target variable — multiclass cancer category |

---

## ⚙️ Modeling Highlights

- **Leakage-free modeling** ensured via feature exclusion.  
- **Cross-validation** with `StratifiedKFold(n_splits=5)` for fair performance averaging.  
- **F1-macro** chosen over accuracy to handle class imbalance.  
- **Top models:**  
  - `LogReg(balanced)` — best for `Risk_Level` (strong minority recall)  
  - `XGBoost` — best for `Cancer_Type` (balanced macro-F1 ~0.77)  
- **Feature signals:** Smoking, Air Pollution, and Obesity rank among the strongest predictors.

---

## 📈 Key Results

| Task | Best Model | Accuracy | F1-Macro |
|------|-------------|----------|----------|
| Cancer_Type | XGBoost | 0.7825 | 0.77 |
| Risk_Level | LogReg(balanced) | 0.83 | 0.73 |

Confusion matrices and permutation importance plots are included for interpretability.

---

## 🧠 Takeaways

- **Leakage detection** is just as important as model tuning — especially in healthcare ML.  
- **Balanced metrics** (F1-macro) give a more realistic picture than accuracy alone.  
- **Interpretability** (via permutation importance) turns models into transparent diagnostic tools.  
- **Modular pipelines** make this notebook directly reusable for other tabular ML tasks.

---


**📂 Explore More:**  
🔗 [Kaggle Profile](https://www.kaggle.com/tarekmasryo) • [GitHub Projects](https://github.com/tarekmasryo) • [LinkedIn](https://www.linkedin.com/in/tarekmasryo)

---
