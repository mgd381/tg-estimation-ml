# Estimating black globe temperature from conventional meteorological variables for WBGT assessment in Lima, Peru.
 
Research repository DOI: [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23308101.svg)](https://doi.org/10.5281/zenodo.23308101)
 
## Overview
 
This repository contains the data, analysis scripts, trained models, and results associated with the study:
 
> Estimating black globe temperature from conventional meteorological variables for WBGT assessment in Lima, Peru.
 
Heat stress assessment using the Wet Bulb Globe Temperature (WBGT) index is limited at conventional meteorological stations that do not measure black globe temperature (Tg). This study developed Multiple Linear Regression (MLR) and Random Forest (RF) models to estimate Tg from air temperature, wind speed, and solar radiation recorded at the Alexander von Humboldt Meteorological Observatory, Universidad Nacional Agraria La Molina, Lima, Peru. Relative humidity was excluded because it added almost no predictive skill, was not statistically significant (p = 0.28) under HAC standard errors, and increased collinearity. Models were trained using daytime observations (10:00–16:00 local time) from January–March 2025, evaluated with five-fold cross-validation grouped by calendar day, and then evaluated independently with data from 20–26 January 2026, a period of elevated temperatures. Solar radiation was the main driver of Tg (r = 0.79), followed by air temperature (r = 0.64). In cross-validation, RF outperformed MLR, with an RMSE of 1.21 °C versus 1.46 °C and an R² of 0.83 versus 0.77. In the independent evaluation, RF achieved an R² of 0.89 and an RMSE of 1.22 °C, whereas MLR yielded 0.81 and 1.62 °C. Both models underestimated the highest Tg values. WBGT computed with estimated Tg agreed closely with the reference WBGT (RMSE of 0.21 °C for RF and 0.29 °C for MLR). These findings support RF as a promising approach for estimating Tg at stations lacking globe thermometers in Lima. However, because both datasets came from a single observatory and covered only daytime hours, transferability across sites, climates, and full diurnal cycles remains to be evaluated.
 
---
 
## Study Area
 
The study was conducted at the **Alexander von Humboldt Meteorological Observatory (AVH)**, located at the **Universidad Nacional Agraria La Molina (UNALM)** in Lima, Peru.
 
Meteorological observations were collected during:
 
- **January–March 2025** (model development and validation)
- **20–26 January 2026** (independent external evaluation)
Only observations recorded between **10:00 AM and 4:00 PM (local time, UTC−5)** were considered, corresponding to the period of maximum solar forcing and greatest heat stress.
 
---
 
## Predictor Variables
 
The predictive models estimate **Black Globe Temperature (Tg)** using the following routinely measured meteorological variables:
 
- Air temperature (T, °C)
- Solar radiation (SR, W m⁻²)
- Wind speed (W, m s⁻¹)
- Relative humidity (RH, %): evaluated during variable selection, but **not included in the final models**. It is still used to estimate the wet-bulb temperature (Stull, 2011) in the WBGT calculation.
Two predictor configurations are compared in the final analysis:
 
| Configuration | Predictors | Role |
|---------------|------------|------|
| **3 variables** | T, W, SR | Final (main) models |
| **4 variables** | T, RH, W, SR | Reference for comparison |
 
---
 
## Methodology
 
The analysis consisted of three sequential stages.
 
### 1. Variable Screening and Selection
 
MLR models were fitted for all 15 combinations of the four predictors and ranked by R² on the validation set (80/20 random split, seed 90). The two best combinations (T–RH–W–SR and T–W–SR) differed by only 0.002 in R², so RH was evaluated further using:
 
- Ordinary Least Squares (OLS) with HAC (heteroskedasticity- and autocorrelation-consistent) standard errors, maximum lag of 12 observations (60 min)
- Variance Inflation Factor (VIF) for both configurations
- Random Forest feature importance
- Correlation analysis
### 2. Predictive Modeling
 
For each configuration (3 and 4 variables), two models were trained:
 
- Multiple Linear Regression (MLR)
- Random Forest Regression (RF): 500 trees, minimum 5 samples per leaf, seed 90, no hyperparameter tuning
The dataset was divided into 80% training and 20% validation (same partition for all models). Model robustness was evaluated using:
 
- 5-fold **GroupKFold** cross-validation, grouped by calendar day (same folds for all models)
- Independent external evaluation using the 2026 dataset (models applied without refitting)
Performance was assessed using R², MAE, and RMSE.
 
### 3. WBGT Error Propagation
 
WBGT was computed with the outdoor equation (0.7·Tnwb + 0.2·Tg + 0.1·T), using observed Tg (reference) and estimated Tg from each model. The thermodynamic wet-bulb temperature (Stull, 2011) is used as a proxy for Tnwb and is identical in all calculations, so differences depend only on Tg.
 
---
 
## Repository Structure
 
```
.
├── analysis/
│   ├── data_analysis.ipynb
│   ├── training_test_analysis_2models.ipynb
│   └── README.md
│
├── data/
│   ├── JFM_2025.csv
│   ├── JAN_2026.csv
│   └── README.md
│
├── results/
│   └── README.md
│
└── README.md
```
 
---
 
## Workflow
 
1. Load the processed meteorological datasets.
2. Perform exploratory data analysis and screening of the 15 predictor combinations.
3. Compare the 3- and 4-variable configurations (HAC significance, VIF, feature importance).
4. Train MLR and RF models for both configurations.
5. Validate models using:
   - 80/20 train/test split
   - 5-fold GroupKFold cross-validation by calendar day
   - Independent 2026 dataset
6. Compare predicted and observed Black Globe Temperature.
7. Estimate WBGT using predicted Tg.
8. Export figures, trained models, and evaluation metrics.
---
 
## Data
 
The repository contains two processed datasets:
 
| Dataset | Purpose |
|----------|---------|
| **JFM_2025.csv** | Model training and internal validation |
| **JAN_2026.csv** | Independent external evaluation |
 
Both datasets have already been preprocessed to include only observations between **10:00 and 16:00 local time**, making them ready for analysis.
 
---
 
## Main Outputs
 
The repository generates:
 
- Exploratory data analysis figures and correlation matrices
- MLR equations (3 and 4 variables)
- Random Forest models (3 and 4 variables)
- GroupKFold cross-validation results
- External validation metrics (2026)
- Observed vs. predicted Tg plots for the 3-variable models (`RF_3vars_plot.png`, `MLR_3vars_plot.png`)
- Estimated WBGT values and error metrics
- Summary table of all models (`model_comparison_3vs4_variables.csv`)
---
 
## Trained Models
 
The trained models are generated automatically by
`analysis/training_test_analysis_2models.ipynb`. Running the notebook
reproduces the four models and saves them in `results/` as `.pkl` files:
 
- `RF_3vars_JFM_2025.pkl`, `MLR_3vars_JFM_2025.pkl` (final models)
- `RF_4vars_JFM_2025.pkl`, `MLR_4vars_JFM_2025.pkl` (comparison models)
---
 
## Requirements
 
Main Python packages used in this project include:
 
- pandas
- numpy
- matplotlib
- scikit-learn
- statsmodels
- scipy
- joblib
---
 
## Citation
 
If you use this repository or its methodology in your work, please cite the associated publication once available.
 
---
 
## License
 
This repository is intended for academic and research purposes.
