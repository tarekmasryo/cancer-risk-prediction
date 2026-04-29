# Case Study — Cancer Risk Classification from Structured Risk Factors

> This case study is for educational ML demonstration only. It is not intended for clinical diagnosis, treatment decisions, or medical advice.

---

## Problem

This project builds a leakage-aware, reproducible baseline for two related tabular classification tasks:

- `Cancer_Type`: multiclass cancer-category classification.
- `Risk_Level`: categorical risk-band classification.

The goal is not to create a clinical system. The goal is to demonstrate a disciplined machine learning workflow for healthcare-style tabular data: data validation, leakage checks, fair evaluation, model comparison, and interpretable diagnostics.

---

## Data

The dataset contains 2,000 patient-level records with demographic fields, lifestyle risk scores, family-history/genetic indicators, clinical indicators, an aggregate risk score, and target labels.

Important fields include:

- `Age`, `BMI`
- `Smoking`, `Alcohol_Use`, `Obesity`
- `Family_History`, `BRCA_Mutation`, `H_Pylori_Infection`
- `Overall_Risk_Score`
- `Risk_Level`
- `Cancer_Type`

---

## Leakage Notes

`Risk_Level` is strongly tied to `Overall_Risk_Score`, so `Overall_Risk_Score` is excluded when training the `Risk_Level` model.

For the `Cancer_Type` task, the notebook also excludes target-derived or task-inappropriate fields to keep the evaluation honest.

Analysis-only columns, such as age bins used for subgroup reporting, are kept out of model features.

---

## Approach

The notebook follows a production-minded baseline workflow:

1. Validate dataset shape, schema, missing values, and target distributions.
2. Establish majority-class baselines.
3. Run focused risk-factor EDA.
4. Build preprocessing pipelines with `ColumnTransformer`.
5. Compare candidate models with stratified cross-validation using macro-F1.
6. Evaluate the selected models on a holdout split.
7. Inspect behavior with classification reports, confusion matrices, calibration curves, permutation importance, and subgroup F1 by age.
8. Export trained pipelines and label encoders for local review.

---

## Models

The candidate model set includes:

- Logistic Regression with class balancing
- Random Forest
- Calibrated Linear SVM
- Gradient Boosting
- XGBoost when available

The primary metric is `F1-macro`, because it gives each class equal weight and is more informative than accuracy when class distributions are imbalanced.

---

## Results Snapshot

| Task | Best Model | Holdout Accuracy | Holdout F1-Macro |
|---|---|---:|---:|
| `Cancer_Type` | XGBoost | 0.783 | 0.764 |
| `Risk_Level` | LogReg(balanced) | 0.830 | 0.727 |

The notebook reports the best-performing baselines for each task and uses permutation importance to inspect which features are most associated with model predictions in this dataset.

---

## Decisions & Takeaways

- Leakage checks are mandatory before model comparison.
- Macro-F1 is the right primary metric for this setup because accuracy can hide minority-class weakness.
- Probability curves should be treated as diagnostics unless models are explicitly calibrated and validated for probability use.
- Permutation importance and confusion matrices make model behavior easier to inspect, but they do not establish clinical causality.
- The workflow is useful as a reusable baseline for structured tabular ML projects.

---

## Limitations

- The dataset is used for educational modeling and should not be interpreted as clinical evidence.
- Performance depends on the dataset quality, label definitions, and feature distributions.
- The notebook does not perform external validation on an independent healthcare dataset.
- Probability outputs should not be used for real-world decisions without stronger calibration, validation, and governance.

---

## Next Steps

- Add a compact `metrics.json` export for easier portfolio and review use.
- Compare calibrated probabilities across candidate models before using probability scores in any decision workflow.
- Add external validation on a separate dataset before considering any real-world healthcare use.
- Package the preprocessing and inference logic into a small reusable script if this project becomes a dashboard or API prototype.
