# Forecasting BitCoin prices using machine learning and TensorFlow

Summary of results by various approaches used

|Model used|MAPE|MAE|
|----------|----|---|
|Naive forecast|2.51|567.98|
|Moving average model|3.12|-|
|ARIMA model|3.15|-|
|Simple Dense model(window=7)|2.54|568.95|
|Simple Dense model(window=30)|2.75|608.26|
|Conv1D model|2.50|561.27|
|LSTM model|2.52|563.12|
|Multivariate model|2.53|567.06|
|N-BEATS model|2.57|574.18|
|Ensemble of deep models|2.58|568.21|


Details of some approaches:

## 1. N-BEATS model:
- This was the most interesting part of the project, where I referred to the N-BEATS paper(available [here](https://github.com/sky-2002/TensorFlow-ML/blob/master/BitPredict/N-BEATS.pdf))
and implemented the N-BEATS architecture in TensorFlow. I read through the paper to understand what each layer and block does.
- The architecture is given below(taken from the paper above):
<img width="800" alt="image" src="https://user-images.githubusercontent.com/84656834/194801366-bbc1d6b0-e690-42b9-ab8e-fe5d4f156938.png">

- Inside the N-BEATS block:
<img width="383" alt="image" src="https://user-images.githubusercontent.com/84656834/194801498-148eef53-ba90-4db3-ac10-2f6be5704bab.png">

##### Note: In the paper, they have used 256 units for the dense layer, but the data scientist in me wanted to experiment and I have thus used 512 units.


## 2. Dense models:
- In this, I experimented with some dense models and also some sequence models like LSTMs.
- I also used 1D convolutional models which performed well.
