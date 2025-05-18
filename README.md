
# Portfolio Dashboard

An end-to-end interactive financial dashboard showcasing data acquisition, transformation, and visualization of stock & ETF performance.

---

## 📊 Project Overview

This repository contains:

* `notebook.ipynb`: A step-by-step Jupyter/Colab notebook that:

  1. **Fetches** historical price data via `yfinance` (Yahoo Finance).
  2. **Cleans & transforms** the data with `pandas`.
  3. **Computes** daily returns, cumulative returns, volatility, and contribution to portfolio return.
  4. **Visualizes** results with a variety of Plotly charts.

* `src/data_prep.py`: A standalone script to download and save adjusted closing prices.

* `src/app.py`: A Streamlit app that wraps the key visualizations into an interactive dashboard.

* `figures/`: Example PNG exports of each chart for quick preview in the README.

---

## 📥 Data Source

* **Library**: [`yfinance`](https://pypi.org/project/yfinance/) (no API key required).
* **Symbols**: `AAPL`, `MSFT`, `GOOG`, `SPY`.
* **Date Range**: January 1, 2024 → May 17, 2025.
* **Frequency**: Daily trading data.
* **Fields**: Adjusted closing price (for total-return accuracy).

The data pipeline is:

1. **Download**: `yfinance.download(tickers, start, end, auto_adjust=True)`.
2. **Save**: Export to `prices.csv` for reproducibility.

---

## 🔄 Analysis Workflow

1. **Load & Inspect**

   * Read `prices.csv` into a `DataFrame`, verify date index and ticker columns.

2. **Daily Returns**

   * Compute `ret = adj_close.pct_change().fillna(0)`.

3. **Cumulative Returns**

   * `cum = (1 + ret).cumprod() - 1` gives total growth since the start date.

4. **Rolling Volatility**

   * `vol30 = ret.rolling(window=30).std()` measures 30-day risk.

5. **Performance Attribution**

   * **Portfolio Weights**: Based on last-date prices or user-defined share counts.
   * **Return Contribution**: `weight * cumulative_return` isolates each holding’s impact.

6. **Correlation Analysis**

   * Pairwise daily-return correlations (AAPL vs SPY, full scatter-matrix).
   * OLS trendlines & R² values to quantify relationships.

---

## 📈 Visualizations

| Figure   | Description                                                     |
| -------- | --------------------------------------------------------------- |
| **Fig1** | Close Price Over Time (range selector + slider, smooth splines) |
| **Fig2** | Cumulative Returns (interactive zoom, % axis)                   |
| **Fig3** | Allocation Pie (1-share basis)                                  |
| **Fig4** | 30-Day Rolling Volatility                                       |
| **Fig5** | Risk vs Return Scatter (bubble size = total return)             |
| **Fig6** | Contribution to Portfolio Return                                |
| **Fig7** | Daily Return Correlation: AAPL vs SPY                           |
| **Fig8** | Scatter Matrix of Daily Returns                                 |

Each chart is first built in the notebook, then integrated into a combined dashboard (Streamlit + Plotly or standalone Plotly subplots).

---

## 🚀 Quickstart

1. **Clone** this repo:

   ```bash
   git clone https://github.com/RaR0014/financial-dashboard.git
   cd portfolio-dashboard
