# Multivariate Time Series Forecasting: VAR vs. LSTM

I explored two different approaches to forecasting multivariate time series data, using the Value, Momentum, Carry, and Defensive factors as examples. I compared the performance of a **Multivariate LSTM** model (multiple output neurons) and a **Vector Autoregression (VAR)** model.

## Data

The monthly return data used in this analysis are from the paper [How Do Factor Premia Vary Over Time? A Century of Evidence](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3400998) by Ilmanen et al. (2019). It explores the following four factor strategies across liquid asset classes:

1. Value
2. Momentum
3. Carry
4. Defensive

![Cumulative Performance of Factors](Cumulative%20Performance%20of%20Factors.png)

## Models

### Vector Autoregression (VAR)

I first applied a VAR model for forecasting the factors, following these steps:

1. Test for stationarity using the Augmented Dickey-Fuller (ADF) test.
2. Fit the VAR model with an optimal lag order, determined by minimizing the BIC.
3. Analyze the model output.
4. Forecast the factors using the fitted model.
5. Evaluate the forecast accuracy using the Mean Absolute Percentage Error (MAPE).

### Multivariate LSTM

Next, I applied a Multivariate LSTM model for forecasting the factorsfollowing these steps:

1. Scale the dataset using the MinMaxScaler.
2. Split the dataset into training and testing sets.
3. Reshape the input data into a 3D array format for the LSTM model.
4. Create and train an LSTM model with Conv1D, Dropout, and Dense layers.
5. (Optional) Perform hyperparameter tuning with 10-fold cross-validation and RandomizedSearchCV.
6. Forecast the factors using the fitted model.
7. Evaluate the forecast accuracy using the Mean Absolute Percentage Error (MAPE).

## Results
![MAPE Comparison](MAPE%20Comparison.png)

## Conclusion

The forecast accuracy for both models was relatively poor. The Multivariate LSTM model performed better for Value and Defensive factors, while the VAR model performed better for Momentum and Carry factors.
Ultimately, the differences in performance are marginal, leading us to go with Occam's Razor and select the simpler model, i.e., the VAR. The fact that a more complex model, like LSTM, does not significantly improve the results could suggest that the features, i.e. past returns, may not be a reliable predictor of future returns, a notion commonly accepted in the field.

**Garbage in, garbage out.**
**You can't math your way out of no alpha.**
