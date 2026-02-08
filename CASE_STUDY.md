# 🧠 Case Study — Cancer Risk Classification (Tabular ML)

## Problem
Build a leakage-aware, reproducible baseline for two related classification tasks:
- **Cancer_Type** (multiclass)
- **Risk_Level** (Low / Medium / High)

The goal is a clean end-to-end notebook that can be reused as a template for healthcare-style tabular ML.

---

## Data
- **File:** `cancer-risk-factors.csv`
- **Grain:** one row per patient
- **Key fields:** demographics, lifestyle factors, clinical/genetic indicators, plus risk-score features

### Leakage note
`Risk_Level` is derived from `Overall_Risk_Score`. To keep evaluation honest, `Overall_Risk_Score` is excluded when training the `Risk_Level` model.

---

## Approach
- **Preprocessing:** numeric/categorical imputation + scaling/one-hot encoding via `ColumnTransformer`
- **Evaluation:** stratified CV with macro-F1 as the primary metric (imbalance-aware)
- **Models:** Logistic Regression, Random Forest, Calibrated Linear SVM, Gradient Boosting, and XGBoost (when available)
- **Interpretability:** confusion matrices + permutation importance for feature signal inspection

---

## Results (snapshot)
The notebook reports the best-performing baselines for each task and highlights the most influential features (e.g., smoking, air pollution, obesity).

---

## Decisions & Takeaways
- Leakage checks are mandatory before any tuning.
- Macro-F1 provides a more realistic view than accuracy for imbalanced clinical labels.
- A modular pipeline (preprocess → model → evaluation) keeps the workflow reusable and less error-prone.

---

## Next Steps
- Add probability calibration comparison across all models (not only SVM).
- Persist a compact `metrics.json` + `best_model.joblib` artifact bundle for deployment demos.
