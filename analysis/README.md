# Analysis

This folder contains the Jupyter notebooks used for exploratory data analysis, feature assessment, model development, and model evaluation.

## Files

### `data_analysis.ipynb`

This notebook performs the exploratory analysis of the meteorological dataset and investigates the relationships between predictor variables and globe temperature (Tg).

The notebook includes:

- Descriptive statistics of all variables.
- Correlation analysis using correlation matrices.
- Visualization of variable relationships.
- Evaluation of different predictor combinations for Multiple Linear Regression (MLR).
- Comparison of regression models based on statistical performance metrics to identify the best predictor set.

---

### `training_test_analysis.ipynb`

This notebook develops, trains, and evaluates the predictive models used in the study.

The notebook includes:

- Training of Random Forest (RF) and Multiple Linear Regression (MLR) models using the 2025 dataset.
- Train-test split evaluation.
- 5-fold cross-validation.
- External validation using the independent 2026 dataset.
- Performance assessment using regression metrics (R², MAE, RMSE, etc.).
- Comparison between observed and predicted globe temperature (Tg).
- Estimation and comparison of WBGT values derived from measured and predicted Tg.
- Statistical assessment of the MLR model using Ordinary Least Squares (OLS).
- Multicollinearity analysis using the Variance Inflation Factor (VIF).
- Generation of the trained Random Forest model (`.pkl`) for later use.
