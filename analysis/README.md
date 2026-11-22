# Analysis
 
This folder contains the Jupyter notebooks used for exploratory data analysis, feature assessment, model development, and model evaluation.
 
## Files
 
### `data_analysis.ipynb`
 
This notebook performs the exploratory analysis of the meteorological dataset and investigates the relationships between predictor variables and globe temperature (Tg).
 
The notebook includes:
 
- Descriptive statistics of all variables.
- Correlation analysis using correlation matrices.
- Visualization of variable relationships.
- Evaluation of the 15 possible predictor combinations for Multiple Linear Regression (MLR), ranked by R² on the validation set.
- Comparison of regression models based on statistical performance metrics, which identified T–RH–W–SR and T–W–SR as the two best-performing combinations and motivated the comparison of the two configurations in `training_test_analysis_2models.ipynb`.
---
 
### `training_test_analysis_2models.ipynb`
 
This notebook develops, trains, and evaluates the predictive models used in the study. Two predictor configurations are compared: **three variables** (T, W, SR; final models) and **four variables** (T, RH, W, SR; reference for comparison).
 
The notebook includes:
 
- Training of Random Forest (RF) and Multiple Linear Regression (MLR) models for both configurations using the 2025 dataset, with the same 80/20 train-test split.
- Train-test split evaluation.
- 5-fold GroupKFold cross-validation, grouped by calendar day, using the same folds for all models.
- External validation using the independent 2026 dataset (models applied without refitting).
- Performance assessment using regression metrics (R², MAE, RMSE).
- Comparison between observed and predicted Tg, with plots for the three-variable RF and MLR models.
- Estimation and comparison of WBGT values derived from measured and predicted Tg, keeping the wet-bulb temperature proxy (Stull, 2011) and air temperature identical.
- Statistical assessment of the MLR predictors using Ordinary Least Squares (OLS) with heteroskedasticity- and autocorrelation-consistent (HAC) standard errors (maximum lag of 12 observations).
- Multicollinearity analysis using the Variance Inflation Factor (VIF) for both configurations.
- A summary table of all models (`model_comparison_3vs4_variables.csv`).
- Generation of the four trained models (`.pkl`: RF and MLR, with three and four variables) for later use.
Outputs are saved in the `results/` folder.
 
