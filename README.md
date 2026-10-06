# Estimation of Black Globe Temperature (Tg) Using Meteorological Variables and Machine Learning

## Overview

This repository contains the data, analysis scripts, trained models, and results associated with the study:

> ** NOMBREDELESTUDIOOOOOOOOOOOOOOOOOO**

AGREGAR EL ABSTRACT ACTUALIZADO

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
- Relative humidity (RH, %)
- Solar radiation (SR, W m⁻²)
- Wind speed (W, m s⁻¹)


---

## Methodology

The analysis consisted of two sequential stages.

### 1. Statistical Variable Selection

Multiple Linear Regression (MLR) models were fitted using every possible combination of predictor variables to determine their statistical significance and identify the most suitable empirical equation.

The statistical evaluation included:

- Multiple Linear Regression (MLR)
- Ordinary Least Squares (OLS)
- p-value significance tests
- Variance Inflation Factor (VIF)
- Correlation analysis

---

### 2. Predictive Modeling

After selecting the statistically significant predictors, two predictive approaches were developed:

- Multiple Linear Regression (MLR)
- Random Forest Regression (RF)

The dataset was divided into:

- 80% training
- 20% validation

Model robustness was evaluated using:

- 5-fold Cross Validation
- Independent external evaluation using the 2026 dataset

Performance was assessed using:

- Coefficient of Determination (R²)
- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)

---

## Repository Structure

```
.
├── analysis/
│   ├── data_analysis.ipynb
│   ├── training_test_analysis.ipynb
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

The complete workflow followed in this repository is:

1. Load the processed meteorological datasets.
2. Perform exploratory data analysis.
3. Evaluate predictor significance using MLR.
4. Train Random Forest and Multiple Linear Regression models.
5. Validate models using:
   - Train/Test split
   - 5-fold Cross Validation
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

- Exploratory data analysis figures
- Correlation matrices
- Multiple Linear Regression equations
- Random Forest models
- Cross-validation results
- External validation metrics
- Observed vs. predicted Tg plots
- Estimated WBGT values
- Performance statistics (R², MAE, RMSE)

---

## Trained Models

The trained Random Forest model is generated automatically by
`analysis/training_test_analysis.ipynb`. Running the notebook
will reproduce the trained model and generate the corresponding `.pkl` file.

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
