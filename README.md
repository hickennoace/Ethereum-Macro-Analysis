# ETH-USD Performance vs BTC, NASDAQ-100, and DXY (2021-2026)

A Jupyter notebook I wrote to figure out how Ethereum actually performed over five years, and whether the "ETH is a USD hedge" story holds up against the data. It's split in two: Part I is ETH against the US Dollar Index (DXY), Part II compares ETH side by side with BTC and the NASDAQ-100.

## What it does

Part I (ETH vs DXY):
- Monthly and annual returns, compounded over 5 years.
- Risk metrics: annualised vol, Sharpe, Sortino, Calmar, max drawdown.
- Correlation and OLS regression vs DXY. Is ETH actually a dollar hedge?
- Rolling 12-month correlation to see if the relationship is stable.

Part II (ETH vs BTC vs NASDAQ-100):
- All four assets rebased to 100 at Jan 2021.
- Annual returns side by side.
- Risk-return scatter with bubble size = |Sharpe|, vs a Capital Market Line at Sharpe = 1.
- Stacked drawdown panels.
- Pairwise correlation heatmap and rolling 12-month correlations.

Each section saves a PNG (`01_*.png` through `13_*.png`).

## Setup

Python 3.9+ should be fine.

```bash
pip install -r requirements.txt
```

Dependencies: numpy, pandas, yfinance, matplotlib, seaborn, scipy.

## How to run

1. Open `main.ipynb` in Jupyter or JupyterLab.
2. Kernel -> Restart & Run All.

Prices are pulled live from Yahoo Finance every time, so you need an internet connection.

## What I'd change if doing it again

All the analysis parameters live in one cell (Part I config in cell 03, Part II tickers in cell 21). The defaults:

```python
START_DATE        = "2021-01-01"
END_DATE          = "2026-01-01"
ETH_TICKER        = "ETH-USD"
DXY_TICKER        = "DX-Y.NYB"
RISK_FREE_ANNUAL  = 0.045
ROLLING_WINDOW    = 12
BTC_TICKER        = "BTC-USD"
NASDAQ_TICKER     = "^NDX"
```

Bump dates or swap tickers there and rerun.

## How I'm computing things

Prices come in daily and get resampled to month-end with `resample("ME").last()`, with a 1-period forward-fill for exchange holidays. From there:

- Simple monthly return: `r_t = P_t / P_{t-1} - 1`
- Log return: `ln(P_t / P_{t-1})`, used for vol and correlation since it's time-additive
- CAGR: `prod(1 + r_t)^(12/n) - 1`
- Annualised vol: `monthly_std * sqrt(12)`
- Sharpe: `(CAGR - Rf) / annual_vol`
- Sortino: `(CAGR - Rf) / downside_vol`
- Calmar: `CAGR / |max_drawdown|`
- Max drawdown: `min((Cumulative - Peak) / Peak)`

For ETH vs DXY: Pearson correlation with a two-tailed t-test, 95% CI via Fisher z, and an OLS regression `r_ETH = alpha + beta * r_DXY + eps`. Rolling correlation uses a 12-month window on log returns.

## What the numbers actually say

Over the 2021-2026 window:

| | ETH | BTC | NASDAQ-100 |
|---|---|---|---|
| Cumulative | +126% | (varies) | +95% |
| CAGR | 18.0% | - | - |
| Annualised vol | 77.8% | - | 19.4% |
| Sharpe | 0.17 | 0.29 | 0.52 |
| Sortino | 0.23 | 0.34 | 0.48 |
| Calmar | 0.23 | 0.30 | 0.44 |
| Max drawdown | -77.0% | -73.0% | -33.0% |

So a few things stand out:

1. ETH beat the NASDAQ-100 on raw return (+126% vs +95%) but with four times the volatility for an extra 3.4 percentage points of CAGR. The Sharpe is the worst of the four assets. An NDX investor captured 81% of ETH's CAGR with 25% of the vol, and never saw a year worse than -33%.

2. ETH against the DXY: correlation is -0.011 with p = 0.934. So statistically zero. "ETH as a dollar hedge" doesn't survive contact with the data. R^2 is 0.0001, beta is -0.12. The dollar explains essentially nothing about ETH's variance.

3. ETH vs BTC: rolling 12-month correlation averages 0.86 and rarely dips below 0.60. Holding both is basically a levered position on the same crypto cycle, not real diversification.

4. ETH vs NASDAQ-100: correlation around 0.61 (p < 0.05), stable across the period. ETH is mostly trading as a risk-on tech proxy, not as something independent.

5. The 18% CAGR is front-loaded. 2021 was +208%. Strip that one year out and 2022-2025 is roughly flat to slightly down. ETH underperformed BTC in both 2023 (+91% vs +155%) and 2024 (+46% vs +121%), and went negative in 2025 (-11%) while NASDAQ-100 gained +20%.

The June 2022 trough was a -77% drawdown that took roughly 18-20 months to recover (back to prior peak around Q1-Q2 2024). Total time underwater across the 60 months was about 26 months.

My read: ETH was worth holding as a small, cycle-timed allocation if you had the discipline for it. As a core or strategic position, it's hard to justify against either BTC or the NASDAQ-100 on a risk-adjusted basis over this window.

## Files

```
main.ipynb              The notebook
requirements.txt        Python deps
01_*.png ... 13_*.png   Output charts
```

## Disclaimer

This is a personal research project. Not financial advice. Past performance doesn't predict future returns, and crypto can lose all of its value.
