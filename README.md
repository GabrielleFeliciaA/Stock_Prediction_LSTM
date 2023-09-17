# Stock Time Series Data Prediction using LSTM Algorithm
Predicting stock prices for every Monday of each week using stock data from previous week's Monday to Friday for `AMZN` Amazon and  `CSCO` Cisco companies. The date range for Amazon stock data is from Thursday, May 15, 1997 to Wednesday, April 1, 2020 and The date range in Cisco stock data spans from Friday, February 16, 1990, to Wednesday, April 1, 2020. The LSTM (Long-Short Term Memory) algorithm is employed for this stock price prediction task. 

## Preprocessing
As the data that is going to be predicted is the stock's closing price, then the only columns that will be used for are the `Date` and `Closed` columns, the other columns will be omitted in each dataset. Each data set presents its own unique challenges, such as incomplete data between Monday and Friday of each week or missing data for Monday predictions. To overcome this, missing data is discarded and not used for predictions. In the data cleaning process, windowing and horizon setting processes are also carried out on the data. Once the data is clean, it is divided into training, testing, and validation data sets.

## Model
The first model that uses the LSTM algorithm has the following architecture:
- Input Layer: The model accepts input with dimensions of 5 neurons
- Lambda Layer: Input is transformed via the Lambda layer into 5 neurons
- LSTM Layer: The results from the Lambda layer are passed to the LSTM layer which produces output with dimensions of 50 neurons
- Output Layer: The output from the LSTM layer is passed to the Dense layer and produces the final output with dimensions of 1 neuron
 
After conducting stock price predictions with the LSTM algorithm, a hyperparameter tuning process is also performed using a custom-built GridSearch function. This involves searching for the optimal hyperparameters, such as batch size, number of epochs, units, optimizer, and activation function, aimed at minimizing error metrics like RMSE, MAE, and MAPE, which serve as evaluation metrics for the model.

After tuning, the best hyperparameter configuration that produces the smallest error for Amazon Dataset is as follows:
- Number of Batches: 16
- Number of Epochs: 150
- Units: 75
- Optimizer: Adagrad
- Number of layers: 1
- Activation Function: Relu
  
And, the tuned model for Amazon Dataset has the following architecture:
- Input Layer: Model receives input with dimensions of 5 neurons
- Lambda Layer: Input is transformed through the Lambda layer into 5 neurons
- LSTM Layer: The results from the Lambda layer are passed to the LSTM layer which produces output with dimensions of 75 neurons
- Output Layer: The output from the LSTM layer is forwarded to the Dense layer and produces the final output with dimensions of 1 neuron


After tuning, the best hyperparameter configuration that produces the smallest error for Cisco Dataset is as follows:
- Number of Batches: 32
- Number of Epochs: 150
- Units: 50
- Optimizer: Adam
- Number of layers: 3
- Activation Function: Relu

And, The tuned model for Cisco Dataset has the following architecture:
- Input Layer: Model receives input with dimensions of 5 neurons
- Lambda Layer: Input is transformed through the Lambda layer into 5 neurons
- LSTM Layer 1: The results of the Lambda Layer become input for LSTM Layer 1, which produces an output with dimensions of 50 neurons
- LSTM Layer 2: The results of LSTM Layer 1 become input for LSTM Layer 2, which produces an output with dimensions of 50 neurons
- LSTM Layer 3: The results of LSTM Layer 2 become input for LSTM Layer 3, which produces an output with dimensions of 50 neurons
- Output Layer: The output from LSTM layer 3 is forwarded to the Dense layer and produces the final output with dimensions of 1 neuron

## Evaluation & Result
Evaluation Metrics Between Baseline and Tuned Model for Amazon Data (Baseline means the first model using the LTSM):
```
	Metric	Baseline	Tuned
0	MAE	21.88553	9.1047735
1	RMSE	27.701843	12.080417
2	MAPE	2.9035044	1.2060512
```

Evaluation Metrics Between Baseline and Tuned Model for Cisco Data (Baseline means the first model using the LTSM):
```
	Metric	Baseline	Tuned
0	MAE	0.21593419	0.21261208
1	RMSE	0.30460057	0.30279186
2	MAPE	0.79343134	0.7791481
```
 
It has been demonstrated that the model using the tuned hyperparameters performs better by producing smaller RMSE, MAE, and MAPE values for both datasets compared to the model with untuned parameters.
