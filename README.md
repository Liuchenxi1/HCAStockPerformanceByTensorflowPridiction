# HCA Healthcare Price Forecast

## Overview

This project uses historical market data, SEC financial data, and machine learning to estimate future HCA Healthcare (`HCA`) stock returns.

The notebook compares:

- Linear Regression
- Ridge Regression
- TensorFlow Neural Network

The main goal is to see whether TensorFlow can improve on simpler regression models and then convert the predicted return into an estimated future HCA stock price.

---

## Market and Technical Elements

| Element | Source | Purpose |
|---|---|---|
| HCA price / volume | Yahoo Finance | Main stock data |
| XLV | Yahoo Finance | Healthcare-sector comparison |
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

SEC data is pulled from the SEC Company Facts API using HCA Healthcare CIK:

```text
0000860730
```

The model uses the SEC **filing date** so financial information is not used before it was publicly available.

| SEC Element | Meaning |
|---|---|
| Total Assets | Size of HCA's asset base |
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
Latest usable date: 2026-05-22
Latest HCA adjusted close: $393.28
```

### End of 2026

```text
Predicted return: -12.8%
Central price estimate: $342.79
Historical residual range: $237.74 - $502.61
```

This means TensorFlow's main prediction is that HCA may decline about **12.8%** from the latest usable price.

The **central price estimate of $342.79** is the model's single best estimate.

The historical residual range shows how large the model's prediction errors were during historical test periods. It is **not** HCA's historical high-low range and is not a guaranteed future range.

A wide range means the model has considerable uncertainty.

---

### End of 2027

```text
Predicted return: +29.6%
Central price estimate: $509.67
Historical residual range: $297.14 - $496.37
```

This means TensorFlow predicts a stronger long-term recovery or increase, with a point estimate near **$509.67**.

The wide historical error range again shows that the forecast has substantial uncertainty.

The current residual-range method can sometimes place the central estimate outside the displayed range, so this part should be improved in a future version.

---

## Important Note About the Latest Usable Date

`2026-05-22` does not mean the HCA market data ends on that date.

It means May 22 is the latest row where all required model features were available at the same time.

If some SEC or growth features are missing after that date, newer market rows cannot currently be used for the final prediction.

Improving this is one of the most important next steps.

---

## The Graph that indicated the 3 different models results: 
<img width="690" height="390" alt="graph 1" src="https://github.com/user-attachments/assets/bcebe831-0033-49c1-aa6f-1037cb5953a2" />
<img width="690" height="390" alt="graph 2" src="https://github.com/user-attachments/assets/ae7a0041-9eb4-4e09-9dfd-a5623591caba" />


