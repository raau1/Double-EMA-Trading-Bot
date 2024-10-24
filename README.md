# Double-EMA-Trading-Bot
Morgan Stanley Coding Challenge - EMA Cross Strategy Trading Bot

# Foreign Exchange Trading Simulation

## Overview
This project was built as part of a programming challenge to develop a forex trading bot for a simulated exchange. My design leverages the Exponential Moving Average (EMA) strategy to analyze market trends and make informed trading decisions.

## Features
- **EMA Trading Strategy**: Implements a dual EMA crossover strategy to identify buy and sell signals based on short-term and long-term trends.
- **Market Data via API**: The bot fetches real-time market data for the EUR/GBP currency pair via an API, enabling it to make decisions with live data.
- **Simulated Market Environment**: The trading bot operates in a simulated forex market, allowing it to assess its performance under realistic conditions.
- **Risk Management**: Includes take-profit and stop-loss mechanisms, maintaining a 2:1 risk-reward ratio to protect against large losses and optimize potential profits.

## How It Works
The bot continuously monitors the EUR/GBP exchange rate via an API and calculates two EMAs (short-term and long-term). A buy signal is generated when the short-term EMA crosses above the long-term EMA, while a sell signal occurs when the short-term EMA crosses below the long-term EMA. Based on these signals, the bot adjusts its positions by either buying or selling currency, while also setting stop-loss and take-profit points to manage risk.

### Exponential Moving Average (EMA)
The EMA is a type of moving average that places greater weight on recent data points, making it more responsive to recent price changes compared to the Simple Moving Average (SMA). The formula for calculating the EMA is:

### Dual EMA Crossover Strategy
The bot uses a **dual EMA crossover** strategy:
- **Short-term EMA**: A fast-moving EMA calculated over a shorter period (e.g., 5 periods) to capture rapid market trends.
- **Long-term EMA**: A slow-moving EMA calculated over a longer period (e.g., 20 periods) to smooth out volatility and capture the broader trend.

The strategy works as follows:
- **Buy Signal**: When the short-term EMA crosses **above** the long-term EMA, it indicates a potential upward trend, and the bot enters a buy position.
- **Sell Signal**: When the short-term EMA crosses **below** the long-term EMA, it suggests a downward trend, and the bot enters a sell position.

By combining these two EMAs, the bot attempts to detect shifts in market momentum, entering trades when short-term trends align with the overall longer-term market direction.

### Code Breakdown
The core logic of the bot is implemented in the `TradingBot` class:
- **Initialization**: The bot is initialized with key parameters such as the currency pair, short and long EMA periods, and risk/reward settings.
- **Fetching Market Data**: The `fetch_latest_price` function retrieves the current market price for the EUR/GBP currency pair from the API and updates the price history.
- **EMA Calculation**: The bot uses Pandas to compute the short and long EMAs based on the price history.
- **Signal Generation**: The `generate_signals` method identifies buy or sell opportunities by analyzing the EMA crossovers.
- **Trade Execution**: The `execute_trade` method sends trade orders to the API based on the identified signals and sets stop-loss and take-profit thresholds using the `set_stop_loss_take_profit` function.
- **Risk Management**: The bot continuously monitors open positions, using stop-loss and take-profit logic to exit trades if predefined conditions are met.

