# Predicting Player Spending Behavior and Profitability in Mobile Games

**Author:** Yuxi Wang

## Overview

This project investigates what drives in-app spending among mobile game players and whether high-value ("whale") users can be identified early. Using a dataset of over 3,000 simulated player records, it builds and evaluates a suite of machine learning models — Lasso regression, decision trees, random forests, XGBoost, and logistic regression — and applies SHAP values to interpret model behavior.

**Key findings:**
- Payment readiness (`PaymentMethod_None`) is the strongest predictor of spending across all models.
- Purchase recency outperforms engagement metrics as a behavioral signal.
- Individual spending amounts are highly noisy (R² = 0–0.10 across all models), but consistent group-level patterns are actionable.
- Whale classification remains difficult with the available features (AUC ≈ 0.583).

---

## Repository Structure

```
MachineLearning/
├── README.md              — this file
├── final_project.qmd      — full analysis in Quarto (Python, plotnine, SHAP, XGBoost)
├── final_project.html     — self-contained rendered HTML report (all figures embedded)
├── paper.pdf              — written final report / paper
├── data/
│   └── initial_data.csv   — original dataset (3,024 player records, 13 columns)
└── figures/               — folder for any exported standalone figures
```

---

## File Descriptions

| File | Description |
|---|---|
| `final_project.qmd` | Quarto source file. Covers data cleaning, feature engineering, EDA (11 figures), five regression models, SHAP analysis, and whale classification. Rendered with `quarto render final_project.qmd`. |
| `final_project.html` | Self-contained HTML output. All figures (Figures 1–22) are embedded. Open directly in any browser — no server required. |
| `paper.pdf` | Written report accompanying the analysis. Describes methodology, results, and business implications. |
| `data/initial_data.csv` | Raw dataset with 3,024 records covering player demographics, gameplay behavior, payment information, and in-app purchase amounts. |
| `figures/` | Directory for any standalone exported figures (e.g., PNG exports of key plots). |

---

## Models and Methods

| Method | Purpose |
|---|---|
| Linear Regression | Baseline (R² ≈ 0.05) |
| Lasso Regression (CV) | Regularized linear model, best R² ≈ 0.10 |
| Decision Tree | Nonlinear splits, interpretable hierarchy |
| Random Forest (300 trees) | Ensemble baseline |
| XGBoost | Gradient boosting with CV-tuned iterations |
| SHAP (TreeExplainer) | Global + local feature attribution |
| Logistic Regression | Whale vs. non-whale classification (AUC ≈ 0.583) |

---

## How to Reproduce

1. Install dependencies:
   ```bash
   pip install pandas numpy scikit-learn xgboost shap plotnine matplotlib
   ```
2. Render the report:
   ```bash
   quarto render final_project.qmd
   ```
   Output: `final_project.html`

---

## Data

`data/initial_data.csv` — 3,024 rows × 13 columns. Key variables:

| Column | Description |
|---|---|
| `InAppPurchaseAmount` | Total spending in USD (regression target) |
| `SessionCount` | Number of gaming sessions |
| `AverageSessionLength` | Average session duration (minutes) |
| `PaymentMethod` | Preferred payment method |
| `GameGenre` | Primary genre played |
| `Country` | Player's country |
| `FirstPurchaseDaysAfterInstall` | Days from install to first purchase |
| `LastPurchaseDate` | Timestamp of most recent purchase |
