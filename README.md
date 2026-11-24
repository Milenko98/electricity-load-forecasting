# Electricity Load Forecasting with a Neural Network

Project for the *Intelligent Infrastructure Systems* course at the **Faculty of Technical Sciences, Novi Sad**.
A desktop application that trains an artificial neural network on historical weather and consumption data and predicts the electricity load for a selected period.

## How it works

1. **Data import** – weather data (temperature, humidity, wind, pressure, cloud cover, conditions…) is loaded from CSV files, cleaned (outliers, missing values, interpolation, categorical encoding) and stored in **SQL Server**.
2. **Training** – the user picks a date range; the data is scaled with `MinMaxScaler`, split 85 / 15 into training and test sets and used to train a **Keras** regression network.
3. **Evaluation** – the model is scored with **MAPE** (mean absolute percentage error) on training and test data.
4. **Prediction** – for a selected period the saved model predicts the load and exports the results to CSV.

## Tech stack

Python · TensorFlow / Keras · pandas · NumPy · scikit-learn · Matplotlib · SQL Server (pyodbc) · Tkinter (tkcalendar)

## Project structure

```
isis/
├── UI.py                 # Tkinter app – import data, choose period, train, predict
├── parse_data.py         # data cleaning and feature preparation
├── create_db.py          # SQL Server connection and tables
├── ann_base.py           # network configuration (layers, neurons, activation, optimizer)
├── ann_regression.py     # model building, training and prediction
├── custom_preparer*.py   # scaling, train/test split and inverse transform
├── scorer.py             # MAPE scoring
└── current_model/        # saved trained model
```

## Running locally

```bash
pip install tensorflow pandas numpy scikit-learn matplotlib pyodbc tkcalendar
cd isis
python UI.py
```

Update the SQL Server connection string in `create_db.py` before the first run.
