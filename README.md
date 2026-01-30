# UniCredit vs. ZABA: daily returns relationship (2015–2025)

## Overview
This project analyzes the relationship between daily stock returns of UniCredit Group (Milan exchange) and Zagrebačka banka (Zagreb Stock Exchange) over 10 years, motivated by the ownership link between the two companies. The workflow includes data collection, cleaning/alignment, statistical testing, correlation analysis, and an OLS regression model.

> Note: The notebook narrative is written in Croatian. This README provides an English summary.

## Data sources
- UniCredit (ticker: UCG.MI): downloaded from Yahoo Finance (via `yfinance` or pre-exported CSV for reliability).
- ZABA: historical prices downloaded from the Zagreb Stock Exchange as CSV.

## Key preprocessing steps
- Convert dates to `datetime` and prices to numeric types.
- Compute daily returns using `pct_change`.
- Remove duplicated ZSE dates caused by different trading models (`CT` vs `BLOCK`) by excluding duplicates.
- Drop rows with `NaN` returns caused by non-overlapping holidays between the two exchanges.
- Remove 2023-01-02 due to Croatia’s HRK→EUR switch (creates an artificial -86% return in the raw series).

## Methods
- Descriptive statistics (mean, std, IQR) for both return series.
- Distribution checks (histograms + QQ-plots) and normality discussion.
- Variance comparison using Bartlett’s test.
- Mean comparison using a two-sample t-test (large-sample justification).
- Covariance and Pearson correlation.
- OLS regression (statsmodels):
  - Dependent variable: ZABA daily returns
  - Independent variable: UCG daily returns (+ intercept)

## Results (high-level)
- The return series are not normally distributed and have different variances.
- Correlation is positive but weak.
- OLS slope is positive and statistically significant; however, the explained variance is very low, so the model is not practically useful for prediction.

## How to run
```bash
pip install -r requirements.txt
jupyter notebook
