# Eaf-heat-temperature-prediction
Machine Learning project for predecting EAF heat temperature using industrial process parametere.

# EAF Heat Temperature Prediction

## Project overview

This project uses industrial Electric Arc Furnace (EAF) process data to predict the final measured bath temperature of a heat.

The problem is different from a finished-product mechanical-property model: here the focus is on an **upstream steelmaking process variable**.

### Objective

Use process information available before the final temperature measurement to estimate the final EAF temperature.

### Data source

Public Kaggle dataset:

**Industrial Data from the Electric Arc Furnace**  
https://www.kaggle.com/datasets/yuriykatser/industrial-data-from-the-arc-furnace

The dataset contains several event tables including:

- EAF temperature and oxidation measurements
- transformer/electrical operation
- basket charging
- additional EAF materials
- carbon injection
- gas and oxygen usage
- chemical measurements
- ladle additions

The complete raw dataset is large, so it should not be committed to the GitHub repository.


## How to run

### Option 1: Google Colab

1. Upload `EAF_Heat_Temperature_Prediction.ipynb`.
2. Run the notebook from the first cell.
3. The notebook uses `kagglehub` to download the public dataset.
4. CSV files are copied into:


## Methodology

### 1. Target definition

For each heat, the last valid temperature measurement is used as the target:

`

### 2. Time-aware feature engineering

Process records are filtered using the target timestamp.

Only records available at or before the target measurement are used.

This is important because using later process measurements would create **target leakage**.

### 3. Features

Examples include:

- initial and previous temperature
- mean/minimum/maximum previous temperature
- number of temperature measurements
- transformer operation count
- total/mean/max MW
- transformer duration
- transformer tap statistics
- oxygen usage and flow
- gas usage and flow
- carbon usage and flow
- basket charge amount
- additional-material amount
- process duration

### 4. Models

The notebook compares:

- Ridge Regression
- Random Forest Regressor
- HistGradientBoosting Regressor

### 5. Evaluation

The models are evaluated using:

- MAE
- RMSE
- R²

The data is ordered by target time and divided into earlier heats for training and later heats for testing.




## Important limitation

This is a data-science prototype using a public industrial dataset. A model used for actual furnace control would require plant-specific validation, sensor-quality checks, operational constraints, safety validation and controlled deployment.

## Suggested CV description

**EAF Heat Temperature Prediction | Python, Pandas, Scikit-learn, Machine Learning**

Developed a time-aware regression pipeline to predict final EAF bath temperature from transformer operation, oxygen/gas usage, carbon injection and charge-material data. Engineered heat-level features from multiple industrial event logs while preventing target leakage through timestamp-based aggregation. Compared regression models using MAE, RMSE and R² and analyzed process-variable importance using permutation importance.

## Interview points

Be ready to explain:

1. Why temperature prediction is useful in an EAF.
2. Why the last temperature measurement was selected as the target.
3. How multiple event tables were joined.
4. Why timestamp filtering was necessary.
5. What target leakage means in this project.
6. Why cumulative oxygen/carbon quantities were not simply summed.
7. Why a time-based train/test split is useful for industrial data.
8. Why MAE and RMSE are both reported.
9. What permutation importance tells us.
10. Why the model should not directly control the furnace without plant validation.

