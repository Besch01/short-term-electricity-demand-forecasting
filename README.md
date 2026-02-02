# Short-Term Electricity Consumption Forecasting

## Overview
This project focuses on short-term (1-hour ahead) forecasting of household electricity consumption using high-frequency energy data. The goal is to build realistic forecasting models while avoiding data leakage and ensuring proper temporal validation.

## Dataset
- Source: [Kaggle – Household Electric Power Consumption](https://www.kaggle.com/datasets/uciml/electric-power-consumption-data-set/data)
- Time span: Dec 2006 – Nov 2010
- Frequency: 1-minute measurements (aggregated to hourly)
- Size: ~2 million observations

The dataset includes global power consumption, voltage, intensity and appliance-level sub-metering. Missing values (~1.25%) were handled via interpolation.

## Exploratory Data Analysis (EDA)
An in-depth EDA was performed to uncover:
- Daily and weekly consumption cycles
- Seasonal patterns across years
- Differences between appliance-level and residual consumption
- Hourly and daily variability

These insights guided feature selection.

## Modeling Approach
Several models were compared using a strict time-based split:

### Baselines
- Random Walk (Persistence)
- Seasonal Naive (same hour, previous year)

### Models
- SARIMA (seasonal statistical baseline)
- XGBoost Regressor (lagged features + calendar features)
- LSTM (single-step recurrent neural network)
- Multi-step LSTM (stacked architecture, used next for 24 hours forecast)

Only information available at prediction time was used.

## Evaluation
Models were evaluated on a held-out test set using:
- MAE
- RMSE
- MAPE

### Key Results
- XGBoost outperformed SARIMA and naive baselines:  
  - MAPE: 42.38%
  - MAE: 316 kWh  
- Single-step LSTM achieved comparable accuracy  
  - MAE: 313 kWh
- Multi-step LSTM in predicting the following 24 hours:
  - MAE: 0.416 kWh

## Libraries
- Python (pandas, numpy, matplotlib, scikit-learn)
- XGBoost
- TensorFlow / Keras
- Statsmodels

## Authors
Academic group project developed as part of the Machine Learning course.  
Contributors: *Matteo Beschi, Quentin Bacher, Paul Prata Leal*
