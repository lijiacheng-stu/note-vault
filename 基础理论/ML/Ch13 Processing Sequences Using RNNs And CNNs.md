## 术语：
- _autocorrelated_:
	- When a time series is correlated with a lagged version of itself, we say that the time series is _autocorrelated_.
- weekly _seasonality_:
	-  a similar pattern is clearly repeated every week
- _naive forecasting_:
	- simply copying a past value to make our forecast.
	- In general, naive forecasting means copying the latest known value (e.g., forecasting that tomorrow will be the same as today). However, in our case, copying the value from the previous week works better, due to the strong weekly seasonality.
- _mean absolute percentage error_ (MAPE):
	- 区别：mean absolute error (MAE)
	- `(diff_7 / targets).abs().mean()`

## 对RNN中的memory cell的理解的理解
-  memory cell = recurrent neuron
- 每次输出一个time step的input，以及上一个状态
- 完成一个样本需要执行window length次
- 