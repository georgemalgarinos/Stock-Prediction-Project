# Stock Price Prediction Using LSTM Neural Network

## Overview

This project demonstrates how to use a Long Short-Term Memory (LSTM) neural network to predict stock prices based on historical data. The model is trained using stock price data fetched from Yahoo Finance. Note: The example used in this code is Mercedes Benz Group AG (MBG.DE), but users can input any valid stock symbol supported by Yahoo Finance.

## Important Disclaimer
The predictions generated by this model are for educational purposes only and should not be considered financial advice. This model is trained on historical data and is not guaranteed to predict future stock prices accurately.

## Features
- Fetch historical stock data using Yahoo Finance.
- Preprocess stock data for model training.
- Build and train an LSTM neural network.
- Predict stock prices and visualize predictions.
- Forecast future stock prices based on the trained model.

## Setup

### Requirements
Ensure you have Python installed. Then, to set up the project, follow these steps:

### 1. Clone the Repository
```
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```
### 2. Set Up a Virtual Environment
To avoid dependency issues, type this.:

 
 ```
python3 -m venv venv
source venv/bin/activate  # For Linux/Mac
```
 **OR**
```
venv\Scripts\activate  # For Windows
```
### 3. Install Dependencies
After activating the virtual environment, install the necessary Python packages by running:
```
pip install -r requirements.txt
```
 If the this doesn't work, install the following packages manually:
```
pip install numpy pandas matplotlib scikit-learn keras yfinance
```
### 4. Edit the Stock Symbol (Optional)
By default, the code fetches data for Mercedes Benz Group AG (MBG.DE). You can change this to any other stock symbol by modifying the stock_symbol variable in the code:
```
stock_symbol = "AAPL"  # For Apple Inc.
```
### The script will:

 - Fetch historical stock data from Yahoo Finance.
 - Preprocess the data.
 - Train an LSTM model on the historical data.
 - Predict future stock prices.
 - Visualize both historical data and the predicted values.

#### Example Output

You will see two visualizations:

#### 1.Historical Stock Data vs. Predictions: A graph showing the actual stock prices alongside the predicted values for both the training and test sets.
#### 2.Future Stock Price Forecast: A graph showing the forecasted stock prices for the next year (365 days).

## Code Breakdown
#### 1. Data Fetching
We use **yfinance** to download historical stock price data:
```
import yfinance as yf
df = yf.download(stock_symbol, start="2010-01-01", end="2023-12-31")
```
You can adjust the start and end dates according to your requirements.

#### 2. Data Preprocessing
We scale the stock prices using MinMaxScaler for optimal model performance and split the dataset into training and testing sets:
```
scaler = MinMaxScaler(feature_range=(0, 1))
data_scaled = scaler.fit_transform(df["Close"].values.reshape(-1, 1))
```
#### 3. LSTM Model
The core of the project is the LSTM neural network built using Keras. The model consists of two LSTM layers and two dense layers:
```
model = Sequential()
model.add(LSTM(50, return_sequences=True, input_shape=(100, 1)))
model.add(LSTM(50, return_sequences=False))
model.add(Dense(25))
model.add(Dense(1))
```
The model is compiled with the Adam optimizer and trained using the **mean_squared_error loss function**.

#### 4. Prediction and Visualization
After training, the model generates predictions for both the training and testing data, which are then plotted:
```
plt.plot(dates, scaler.inverse_transform(data_scaled), label='Original Data', color='blue')
plt.plot(train_dates, train_predict, label='Training Predictions', color='green')
plt.plot(test_dates, test_predict, label='Test Predictions', color='red')
```
#### 5. Future Predictions
The model can predict stock prices for future dates, which are then visualized in a separate plot:
```
num_prediction = 365  # Predict for the next 365 days
forecast = predict_future(num_prediction, model)
forecast_dates = predict_dates(num_prediction)
```
## Important Notes
This model does not provide financial advice. Predictions are based on past performance and should not be interpreted as guarantees of future performance.
Stock data can and will fluctuate based on external factors, and this model is only trained on historical data.


































