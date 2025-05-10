## Hi there 👋

<!--
**Deepak6380/Deepak6380** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.arima.model import ARIMA
import yfinance as yf
import warnings
warnings.filterwarnings("ignore")

# Step 1: Download stock data
stock_symbol = 'AAPL'  # Replace with actual ticker, e.g., 'AL-DITVEN' if available
data = yf.download(stock_symbol, start='2020-01-01', end='2024-12-31')
prices = data['Close']

# Step 2: Plot historical closing prices
plt.figure(figsize=(12, 5))
plt.plot(prices, label='Close Price', color='blue')
plt.title(f'{stock_symbol} Stock Price (2020–2024)')
plt.xlabel('Date')
plt.ylabel('Price (USD)')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()

# Step 3: Fit ARIMA model (adjust p,d,q as needed)
model = ARIMA(prices, order=(5, 1, 0))
model_fit = model.fit()

# Step 4: Forecast next 30 days
forecast = model_fit.forecast(steps=30)

# Step 5: Plot forecast
plt.figure(figsize=(12, 5))
plt.plot(prices[-100:], label='Recent Prices', color='blue')
plt.plot(forecast.index, forecast, label='30-Day Forecast', color='red')
plt.title(f'{stock_symbol} Stock Price Forecast')
plt.xlabel('Date')
plt.ylabel('Price (USD)')
plt.grid(True)
plt.legend()
plt.tight_layout()
plt.show()
