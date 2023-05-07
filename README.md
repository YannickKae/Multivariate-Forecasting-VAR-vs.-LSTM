# Multivariate Time Series Forecasting: VAR vs. LSTM

In this project, we explore two different approaches to forecasting multivariate time series data, using the Value, Momentum, Carry, and Defensive factors as examples. I compare the performance of a **Multivariate LSTM** model (multiple output neurons) and a **Vector Autoregression (VAR)** model.

## Data

The monthly return data used in this analysis are from the paper [How Do Factor Premia Vary Over Time? A Century of Evidence](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3400998) by Ilmanen et al. (2019). It explores the following four factor strategies across liquid asset classes:

1. Value
2. Momentum
3. Carry
4. Defensive

![Cumulative Performance of Factors](Cumulative%20Performance%20of%20Factors.png)

## Models

### Vector Autoregression (VAR)

I first applied a VAR model for forecasting the factors. I followed these steps:

1. Test for stationarity using the Augmented Dickey-Fuller (ADF) test.
2. Fit the VAR model with an optimal lag order, determined by minimizing the BIC.
3. Analyze the model output.
4. Forecast the factors using the fitted model.
5. Evaluate the forecast accuracy using the Mean Absolute Percentage Error (MAPE).

### Multivariate LSTM

Next, I applied a Multivariate LSTM model for forecasting the factors. We followed these steps:

1. Scale the dataset using the MinMaxScaler.
2. Split the dataset into training and testing sets.
3. Reshape the input data into a 3D array format for the LSTM model.
4. Create and train an LSTM model with Conv1D, Dropout, and Dense layers.
5. (Optional) Perform hyperparameter tuning with 10-fold cross-validation and RandomizedSearchCV.
6. Forecast the factors using the fitted model.
7. Evaluate the forecast accuracy using the Mean Absolute Percentage Error (MAPE).

## Results

I compared the MAPE of the LSTM and VAR models for each factor. The results were as follows:

- Value: LSTM (0.8390) vs. VAR (0.8861)
- Momentum: LSTM (0.8975) vs. VAR (0.8803)
- Carry: LSTM (1.2852) vs. VAR (1.2089)
- Defensive: LSTM (0.9684) vs. VAR (1.1312)

In general, the forecast accuracy for both models was relatively poor. The Multivariate LSTM model performed better for Value and Defensive factors, while the VAR model performed better for Momentum and Carry factors.

## Conclusion

Both the Multivariate LSTM and VAR models have their strengths and weaknesses, and neither model provided consistently accurate forecasts across all factors. Further research and model tuning may be necessary to improve the forecast accuracy for these factors. Additionally, other models, such as Bayesian structural time series models or machine learning algorithms like XGBoost, could be explored to find a more suitable forecasting approach for this dataset.
