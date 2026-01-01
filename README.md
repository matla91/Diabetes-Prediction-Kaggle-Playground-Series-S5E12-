# Diabetes Prediction – Kaggle Playground Series (S5E12)

This repository presents my participation in the Kaggle *Playground Series Season 5 – Episode 12* competition, focused on **diabetes risk prediction using tabular medical and lifestyle data**.

The objective of this project is **not leaderboard maximization**, but rather:
- rigorous data analysis,
- realistic performance assessment,
- and a methodology aligned with real-world machine learning constraints.

---

## 🎯 Project Objectives

This project aims to:

- Perform a **thorough and honest Exploratory Data Analysis (EDA)**
- Identify **structural limitations of the dataset before modeling**
- Build a **strong, well-validated baseline model**
- Prioritize **robustness, interpretability, and calibration** over marginal metric gains
- Explicitly avoid leaderboard overfitting and validation leakage

This notebook reflects how I would approach a **real-world applied ML problem**, not a Kaggle-only optimization task.

---

## 📊 Dataset Overview

- **Source**: Kaggle Playground Series (synthetic data)
- **Samples**:
  - Train: 700,000 rows
  - Test: 300,000 rows
- **Target**: `diagnosed_diabetes` (binary classification)
- **Features**:
  - Demographic (age, gender, ethnicity)
  - Lifestyle (physical activity, diet score, sleep, smoking)
  - Clinical proxies (BMI, blood pressure, cholesterol)

⚠️ **Important limitation**:  
The dataset does **not include primary causal biomarkers** for diabetes (e.g. fasting glucose, HbA1c, insulin).  
All predictive power comes from **indirect clinical proxies**, which strongly constrains achievable performance.

Due to Kaggle rules, the dataset is **not included** in this repository.

---

## 🧠 Methodological Scope

This notebook intentionally focuses on:

- Understanding **signal vs. synthetic noise**
- Detecting **class overlap and performance ceilings**
- Evaluating **train/test covariate shift**
- Interpreting model behavior rather than blindly optimizing scores

### What this notebook deliberately avoids:
- Leaderboard probing
- Validation leakage
- Aggressive feature engineering
- Blind ensembling

---

## 🔍 Exploratory Data Analysis Highlights

Key EDA insights include:

- **Strong class overlap** across all major features
- Biological consistency checks (e.g. BMI vs Waist-to-Hip Ratio correlation)
- Detection of **synthetic artifacts** (grid-like feature distributions)
- Statistical **covariate shift between train and test sets** (KS-tests)
- Identification of a **realistic ROC-AUC ceiling (~0.72–0.73)** before modeling

The EDA directly guides modeling choices and prevents unrealistic expectations.

---

## 🤖 Modeling Strategy

- **Problem type**: Binary classification
- **Metric**: ROC-AUC (robust to class imbalance, threshold-free)
- **Validation**: 5-Fold Stratified Cross-Validation
- **Model**: LightGBM (controlled complexity, strong regularization)

Key principles:
- Minimal feature engineering
- Strong regularization to mitigate synthetic noise
- No hyperparameter over-optimization

This approach favors **generalization stability** over leaderboard exploitation.

---

## 📈 Results

- **Out-of-Fold ROC-AUC**: ~0.727
- Very low variance across CV folds
- Performance consistent with known limits of proxy-based diabetes datasets

This confirms that the observed ceiling is **data-driven**, not model-driven.

---

## 🔎 Interpretability & Error Analysis

The notebook includes:

- **SHAP-based feature importance**
- Clinical error profiling:
  - False Negatives concentrated in *younger, lean patients*
  - False Positives biased toward *older, higher-BMI profiles*
- Explicit identification of **model blind spots**
- **Uncertainty analysis**:
  - ~16% of predictions are intrinsically ambiguous
- **Probability calibration analysis** (reliability diagram, Brier score)

These analyses mirror how models should be evaluated in **healthcare-adjacent or high-risk domains**.

---

## ⚠️ Limitations

- Absence of causal biomarkers
- Synthetic data generation artifacts
- Global covariate shift between train and test
- High class overlap limits discriminative power

Further gains are possible but would likely rely on **dataset-specific artifacts**, not meaningful signal.

---

## 🚀 What This Project Demonstrates

This project showcases:

- End-to-end ML pipeline on large-scale tabular data
- Strong EDA driving modeling decisions
- Awareness of validation bias and distribution shift
- Model interpretability and ethical error analysis
- The ability to **know when not to optimize further**

Understanding data limitations is as important as building powerful models.

---

## 🧪 Potential Extensions (Not Implemented)

- Adversarial validation
- Sample reweighting
- Feature interaction modeling
- Lightweight ensemble for stability

These were intentionally excluded to preserve methodological integrity.

---

## 📂 Repository Structure

