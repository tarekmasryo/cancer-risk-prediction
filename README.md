# 🧬 Cancer Risk Classification — From Risk Factors to Validated ML Baselines

**Author:** [Tarek Masryo](https://www.kaggle.com/tarekmasryo)  
**License:** MIT for repository code. Dataset usage follows the original Kaggle dataset license.

---

## 📘 Project Overview

A clean, reproducible machine learning notebook for cancer-type and risk-level classification from structured patient risk-factor data.

The goal is to demonstrate a transparent educational workflow:

data understanding → leakage checks → feature preprocessing → model benchmarking → diagnostics.

This project is for educational and analytical purposes only. It is not intended for clinical diagnosis, treatment decisions, or medical advice.

---

## 🧩 Pipeline Summary

| Stage | Description |
|---|---|
| Dataset card & validation | Shape checks, schema review, missing-value checks, target distributions, and majority-class baselines |
| Risk-factor EDA | Age/BMI bins, lifestyle risk-score patterns, and relationships with `Risk_Level` |
| Leakage checks | Explicit handling of `Risk_Level`, `Overall_Risk_Score`, and analysis-only columns before modeling |
| Preprocessing | Numeric imputation + scaling, categorical imputation + one-hot encoding via `ColumnTransformer` |
| Model comparison | Cross-validated macro-F1 scoring for Logistic Regression, Random Forest, Calibrated Linear SVM, Gradient Boosting, and XGBoost |
| Diagnostics | Confusion matrices, calibration curves, permutation importance, and subgroup F1 by age |
| Artifacts | Exported trained pipelines and label encoders under `artifacts/` |

---

## 📊 Dataset

**File:** `cancer-risk-factors.csv`  
**Rows:** 2,000 patient records  
**Columns:** demographics, lifestyle risk scores, family history/genetic indicators, clinical indicators, and target labels

| Feature | Description |
|---|---|
| `Age`, `BMI` | Demographic and body-mass metrics |
| `Smoking`, `Alcohol_Use`, `Obesity` | Lifestyle risk scores on a 0–10 scale |
| `Family_History`, `BRCA_Mutation`, `H_Pylori_Infection` | Family-history, genetic, and clinical indicator fields |
| `Overall_Risk_Score` | Numeric aggregate risk score; excluded when modeling `Risk_Level` |
| `Risk_Level` | Categorical risk band used as one modeling target |
| `Cancer_Type` | Multiclass cancer-category label used as one modeling target |

---

## ⚙️ Modeling Highlights

- Leakage-aware feature selection for both modeling tasks.
- `StratifiedKFold(n_splits=5)` cross-validation for class-balanced evaluation.
- `F1-macro` as the primary metric to avoid over-rewarding majority-class performance.
- Holdout evaluation with classification reports and confusion matrices.
- Probability diagnostics through calibration curves.
- Permutation importance for feature-signal inspection.
- Subgroup F1 reporting by age bin for additional reliability checks.

---

## 📈 Key Results

| Task | Best Model | Holdout Accuracy | Holdout F1-Macro |
|---|---|---:|---:|
| `Cancer_Type` | XGBoost | 0.783 | 0.764 |
| `Risk_Level` | LogReg(balanced) | 0.830 | 0.727 |

These results should be treated as dataset-specific educational baselines, not clinical evidence.

---

## 🧠 Takeaways

- Leakage checks matter as much as model choice in healthcare-style tabular ML.
- Macro-F1 gives a more honest view than accuracy when class distributions are imbalanced.
- Permutation importance and confusion matrices make model behavior easier to inspect.
- A modular preprocessing-and-modeling pipeline makes the workflow reusable for other tabular classification tasks.

---

## 📁 Repository Layout

```text
.
├── cancer-risk-factors-prediction.ipynb
├── README.md
├── CASE_STUDY.md
├── LICENSE
├── requirements.txt
├── .gitignore
├── data/
│   └── raw/
│       └── .gitkeep
├── artifacts/
│   └── .gitkeep
└── archive/
    ├── README.md
    └── cancer-risk-factors-prediction.ipynb
```

`archive/` is kept for reference only. The active notebook version is located at the repository root.

---

## ⚡ Quick Start

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate

pip install -r requirements.txt
```

Place the dataset file under:

```text
data/raw/cancer-risk-factors.csv
```

On Kaggle, attach the dataset to the notebook and update the dataset path cell if needed.

---

## 📈 Outputs & Artifacts

The notebook can export the following files under `artifacts/`:

```text
artifacts/cancer_type_model.joblib
artifacts/cancer_type_label_encoder.joblib
artifacts/risk_level_model.joblib
artifacts/risk_level_label_encoder.joblib
```

These artifacts are useful for local review and portfolio demonstration. They should be externally validated before any real-world use.

---

## 🧾 Case Study

See [`CASE_STUDY.md`](CASE_STUDY.md) for the project story, modeling decisions, limitations, and next steps.

---

## 🔗 Explore More

- [Kaggle Profile](https://www.kaggle.com/tarekmasryo)
- [GitHub Projects](https://github.com/tarekmasryo)
- [LinkedIn](https://www.linkedin.com/in/tarekmasryo)
