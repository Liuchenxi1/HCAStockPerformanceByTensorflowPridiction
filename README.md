# Stock Price Forecast

## Overview

This project uses historical market data, SEC financial data, and machine learning to estimate future stock returns.

The notebook compares:

- Linear Regression
- Ridge Regression
- TensorFlow Neural Network

The main goal is to see whether TensorFlow can improve on simpler regression models and then convert the predicted return into an estimated future Ticker stock price.

# How to Use

Enter a ticker at the top of the notebook: "Enter the stock ticker to analyze (example: AAPL, MSFT, HCA): "

The default benchmark is:

BENCHMARK_TICKER = "SPY"

You can replace SPY with a sector ETF if you want a more specific benchmark.

---

## Market and Technical Elements

| Element | Source | Purpose |
|---|---|---|
| Ticker price / volume | Yahoo Finance | Main stock data |
| Benchmark | Yahoo Finance | SPY price and return |
| VIX | Yahoo Finance | Market fear / volatility |
| 3M Treasury | Yahoo Finance | Short-term interest-rate environment |
| 10Y Treasury | Yahoo Finance | Long-term interest-rate environment |
| Moving averages | Calculated | Price trend |
| RSI | Calculated | Momentum / overbought-oversold signal |
| MACD | Calculated | Trend and momentum |
| Volatility | Calculated | Recent stock risk |
| Money Flow | Calculated | Estimated buying / selling pressure |
---

## SEC Fundamental Elements

The notebook automatically looks up the SEC CIK for the selected ticker and then downloads Company Facts data.

The model uses the SEC **filing date** so financial information is not used before it was publicly available.

| SEC Element | Meaning |
|---|---|
| Total Assets | Company asset base |
| Total Liabilities | Total obligations |
| Cash | Available cash |
| Total Debt | Current and long-term debt |
| Stockholders' Equity | Book equity |
| Revenue | Company sales |
| Net Income | Profit |
| Operating Cash Flow | Cash generated from operations |
| Capital Expenditures | Investment in property/equipment |
| Free Cash Flow | Operating Cash Flow minus CapEx |
| Debt to Assets | Debt relative to assets |
| Cash to Debt | Cash relative to debt |
| FCF Margin | Free cash flow relative to revenue |
| Growth Features | Changes in revenue, profit, assets, liabilities, and FCF |

---

## Model Comparison

All models use the same chronological train, validation, and test periods.

| Model | Purpose |
|---|---|
| Linear Regression | Simple baseline for linear relationships |
| Ridge Regression | Linear model with regularization to reduce overfitting |
| TensorFlow Neural Network | Captures nonlinear relationships and interactions |

The models are compared using:

| Metric | Meaning | Better |
|---|---|---|
| MAE | Average prediction error | Lower |
| RMSE | Penalizes large prediction errors | Lower |
| R² | How much variation the model explains | Higher |

The best model should be chosen from the **test results**, not simply because TensorFlow is more advanced.

Train / Validation / Test Split

The data is split chronologically:

Oldest                                         Newest
---------------------------------------------------->

|       Train 70%       | Validation 15% | Test 15% |

There is no random shuffle.

---

## Forecast Logic

The model predicts a future return:

```text
Future Return =
Future HCA Price / Current HCA Price - 1
```

The predicted return is converted into a future price:

```text
Predicted Price =
Current HCA Price × (1 + Predicted Return)
```

---

## Current TensorFlow Results

```text
The final output looks like:

TICKER PRICE FORECAST SUMMARY
========================================

Latest market date: YYYY-MM-DD
Latest adjusted close: $XXX.XX

TensorFlow — target YYYY-12-31
Predicted return: XX.X%
Central price estimate: $XXX.XX
Historical residual range: $XXX - $XXX
```

Central Price Estimate: The model's main point forecast.

Example: The **central price estimate of $342.79** is the model's single best estimate.

The notebook uses these historical errors to estimate a wider forecast range. This does not mean the stock's historical low and high.

It means the model historically had prediction errors large enough to create that range around the current forecast.

A wider range means more uncertainty.

---


## The Graph that indicated the 3 different models results: 
<img width="689" height="390" alt="image" src="https://github.com/user-attachments/assets/e31110b8-868e-4bb0-8e28-640b0d7b2f4d" />
<img width="690" height="390" alt="image" src="https://github.com/user-attachments/assets/375d19d2-c686-4d48-a110-12b48993120d" />



