# ETH-USD Performance Analysis: BTC & NASDAQ-100 Comparison (2021–2026)

A production-grade Jupyter Notebook for quantitative analysis of Ethereum's performance over a 5-year period. The analysis is split into two parts: a deep-dive into ETH vs the US Dollar Index (DXY), followed by a comprehensive multi-asset comparison benchmarking ETH against Bitcoin (BTC) and the NASDAQ-100.

---

## Overview

### Part I — ETH vs USD (DXY)
1. **How did ETH perform?** — Monthly and annual returns, compounded over 5 years.
2. **How risky was it?** — Volatility, Sharpe, Sortino, Calmar ratios, and maximum drawdown.
3. **Is ETH a USD hedge?** — Statistical correlation and OLS regression against the US Dollar Index (DXY).

### Part II — ETH vs BTC vs NASDAQ-100
4. **How does ETH compare to Bitcoin?** — Side-by-side risk/reward across the full crypto cycle.
5. **How does ETH compare to tech equities?** — Is the volatility premium over NASDAQ-100 justified by returns?
6. **Are the assets correlated?** — Pairwise correlation heatmap and rolling co-movement over time.

---

## Features

### Part I — ETH / DXY Analysis

| Feature | Description |
|---------|-------------|
| Monthly Returns | Simple percentage return for each calendar month |
| Annual Returns | Geometric mean (CAGR) and arithmetic mean per year |
| Rolling Volatility | 12-month annualised standard deviation |
| Sharpe Ratio | Return per unit of total risk vs. risk-free rate |
| Sortino Ratio | Return per unit of **downside** risk only |
| Calmar Ratio | CAGR divided by maximum drawdown |
| Max Drawdown | Largest peak-to-trough decline over the period |
| Pearson Correlation | ETH vs DXY monthly return correlation with p-value |
| Fisher Z CI | 95% confidence interval for the correlation coefficient |
| OLS Regression | Beta (sensitivity) and Alpha (excess return) of ETH vs DXY |
| Rolling Correlation | 12-month sliding window correlation between ETH and DXY |

### Part II — Multi-Asset Comparison

| Feature | Description |
|---------|-------------|
| Normalized Returns | All assets rebased to 100 at Jan 2021 for a common comparison |
| Annual Return Comparison | Year-by-year CAGR for ETH, BTC, and NASDAQ-100 |
| Risk–Return Scatter | Volatility vs CAGR bubble chart with |Sharpe| as bubble size |
| Multi-Asset Drawdown | Stacked underwater panels for ETH, BTC, and NASDAQ-100 |
| Pairwise Correlation Heatmap | Full correlation matrix with significance markers |
| Rolling Correlations | 12-month ETH–BTC and ETH–NASDAQ-100 rolling ρ |
| Metrics Summary Table | Side-by-side table of all six risk metrics for all four assets |

---

## Visualisations

### Part I

| Plot | Output File | Question Answered |
|------|-------------|-------------------|
| 1. Cumulative Return — ETH vs DXY | `01_cumulative_returns.png` | How did $1 grow over 5 years? |
| 2. Monthly Return Heatmap | `02_monthly_heatmap.png` | Which months/years were good or bad? |
| 3. Annual Returns Bar Chart | `03_annual_returns.png` | How did yearly returns evolve? |
| 4. Rolling Volatility & Sharpe | `04_rolling_vol_sharpe.png` | How did risk efficiency change over time? |
| 5. Drawdown Underwater Chart | `05_drawdown.png` | How deep and long were bear markets? |
| 6. Correlation Dashboard | `06_correlation_dashboard.png` | What is the ETH–DXY statistical relationship? |

### Part II

| Plot | Output File | Question Answered |
|------|-------------|-------------------|
| 7. Normalized Cumulative Returns | `07_normalized_cumulative.png` | How did all assets grow from a common base? |
| 8. Annual Returns Comparison | `08_annual_comparison.png` | Were crypto and equity gains in the same years? |
| 9. Risk–Return Scatter | `09_risk_return.png` | Where does each asset sit on the vol–reward curve? |
| 10. Multi-Asset Drawdown | `10_multi_drawdown.png` | How did bear-market depth and timing compare? |
| 11. Pairwise Correlation Heatmap | `11_correlation_heatmap.png` | How closely do the four assets co-move? |
| 12. Rolling Correlations | `12_rolling_correlations.png` | Has the ETH–BTC / ETH–NASDAQ relationship shifted? |
| 13. Performance Metrics Table | `13_metrics_table.png` | Side-by-side summary of all key measures |

---

## Project Structure

```
JupyterProject/
│
├── main.ipynb                    # Main Jupyter Notebook (50 cells)
├── README.md                     # This file (English)
├── README_HE.md                  # Hebrew README
├── requirements.txt              # Python dependencies
│
├── 01_cumulative_returns.png
├── 02_monthly_heatmap.png
├── 03_annual_returns.png
├── 04_rolling_vol_sharpe.png
├── 05_drawdown.png
├── 06_correlation_dashboard.png
│
├── 07_normalized_cumulative.png
├── 08_annual_comparison.png
├── 09_risk_return.png
├── 10_multi_drawdown.png
├── 11_correlation_heatmap.png
├── 12_rolling_correlations.png
└── 13_metrics_table.png
```

---

## Requirements

Python **3.9+** is recommended.

Install all dependencies with:

```bash
pip install -r requirements.txt
```

| Library | Version (minimum) | Purpose |
|---------|--------------------|---------|
| `numpy` | ≥ 1.24 | Numerical computation |
| `pandas` | ≥ 2.0 | Time-series data manipulation |
| `yfinance` | ≥ 0.2 | Yahoo Finance price data |
| `matplotlib` | ≥ 3.7 | Core plotting engine |
| `seaborn` | ≥ 0.12 | Statistical visualisations |
| `scipy` | ≥ 1.10 | Pearson correlation, OLS regression |

---

## How to Run

1. Clone or download the repository.
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Open `main.ipynb` in Jupyter Notebook or JupyterLab.
4. Run all cells top-to-bottom:
   `Kernel → Restart & Run All`

> **Note:** All price data is fetched live from Yahoo Finance on each run.
> An active internet connection is required.

---

## Configuration

All parameters are centralised in **Cell 03** of the notebook (Part I config) and **Cell 21** (Part II tickers). No other cell needs to be edited:

**Part I — Cell 03**
```python
START_DATE        = "2021-01-01"   # Analysis start date (inclusive)
END_DATE          = "2026-01-01"   # Analysis end date (exclusive)
ETH_TICKER        = "ETH-USD"      # Primary asset — Ethereum in USD
DXY_TICKER        = "DX-Y.NYB"    # USD proxy — ICE Dollar Index
RISK_FREE_ANNUAL  = 0.045          # 4.5% — 3M T-bill average over the period
ROLLING_WINDOW    = 12             # Months for all rolling calculations
```

**Part II — Cell 21**
```python
BTC_TICKER        = "BTC-USD"      # Bitcoin in USD
NASDAQ_TICKER     = "^NDX"         # NASDAQ-100 Index
```

---

## Methodology

### Price Data
- Source: **Yahoo Finance** via `yfinance` with `auto_adjust=True`
- Frequency: Daily closes, resampled to **month-end** using the last observed price
- Forward-fill limit of 1 day applied to handle exchange holidays
- Part II uses a generic `build_multi_asset_prices()` that aligns any number of daily series onto a shared month-end calendar

### Return Calculations

| Formula | Description |
|---------|-------------|
| `r_t = (P_t / P_{t-1}) - 1` | Simple monthly return |
| `ln_r_t = ln(P_t / P_{t-1})` | Log return (used for volatility & correlation) |
| `CAGR = ∏(1 + r_t)^(12/n) - 1` | Compounded annual growth rate |

### Risk Metrics

| Metric | Formula |
|--------|---------|
| Annualised Vol | `σ_monthly × √12` |
| Sharpe | `(CAGR − Rf) / σ_annual` |
| Sortino | `(CAGR − Rf) / σ_downside` |
| Calmar | `CAGR / |Max Drawdown|` |
| Max Drawdown | `min((Cumulative − Peak) / Peak)` |

### Correlation Analysis

| Step | Method |
|------|--------|
| Full-period correlation | Pearson ρ on monthly simple returns |
| Significance test | Two-tailed t-test: `t = ρ√((n−2)/(1−ρ²))` |
| Confidence interval | Fisher Z-transform → back-transform to ρ scale |
| Regression | OLS: `r_ETH = α + β·r_DXY + ε` |
| Rolling correlation | 12-month sliding window on log returns |
| Pairwise heatmap (Part II) | Pearson ρ on log returns for all four assets |

### Asset Selection

| Asset | Ticker | Rationale |
|-------|--------|-----------|
| Ethereum | `ETH-USD` | Primary subject of analysis |
| Bitcoin | `BTC-USD` | Dominant crypto — natural peer benchmark |
| NASDAQ-100 | `^NDX` | Tech-equity benchmark — tests whether ETH's vol premium is justified vs high-growth equities |
| DXY | `DX-Y.NYB` | ICE Dollar Index — geometrically weighted basket of USD vs EUR, JPY, GBP, CAD, SEK, CHF |

---

## Interpreting the Results

### Part I — ETH vs DXY

| Result | Financial Interpretation |
|--------|--------------------------|
| `ρ < 0` and `p < 0.05` | ETH is a **statistically significant** inverse of USD — a potential hedge |
| `β < 0` | ETH moves **opposite** to the dollar on a monthly basis |
| `α > 0` (annualised) | ETH earns **excess return** independent of USD movements |
| High Sortino vs. Sharpe | Return distribution is **positively skewed** — large gains dominate |
| Calmar > 1 | Each unit of drawdown risk produced more than 1 unit of return |

### Part II — Multi-Asset

| Result | Financial Interpretation |
|--------|--------------------------|
| ETH–BTC ρ close to 1 | ETH and BTC behave as the **same asset class** — diversification benefit is limited |
| Rising ETH–NASDAQ ρ over time | Crypto is increasingly **trading as a risk-on equity proxy** |
| ETH above CML in Plot 9 | ETH delivered a Sharpe > 1.0 — outperformed on a risk-adjusted basis |
| Synchronised drawdowns in Plot 10 | Bear markets were driven by **shared macro shocks**, not asset-specific events |

---

## Conclusions

The following conclusions are derived exclusively from the quantitative evidence produced by this analysis — 59 monthly observations of ETH-USD price data from January 2021 to January 2026, benchmarked against Bitcoin, the NASDAQ-100, and the US Dollar Index.

---

### 1. Investment Worthiness — Risk-Reward vs. Alternatives

On a raw return basis, ETH outperformed both the NASDAQ-100 and the DXY, delivering a cumulative **+126%** (CAGR 18.0%) versus +95% for the NASDAQ-100 and +9% for the DXY. However, the investment case weakens substantially once volatility is accounted for.

ETH's annualised volatility of **77.8%** is four times that of the NASDAQ-100 (19.4%), yet the incremental CAGR advantage over tech equities is only **+3.4 percentage points**. The Sharpe ratio of **0.17** — versus 0.52 for the NASDAQ-100 and 0.29 for BTC — places ETH as the worst risk-adjusted performer among all benchmarked assets. An investor in the NASDAQ-100 captured 81% of ETH's geometric CAGR while absorbing just 25% of its volatility, and did so without a single calendar year exceeding a −33% loss.

The one dimension where ETH's risk is genuinely compensated is the **absolute return premium over traditional assets during bull cycles**. In 2021 alone, ETH returned +208% — a gain inaccessible through any conventional instrument. For investors with a high risk tolerance and the discipline to size positions accordingly, ETH provided asymmetric upside that no alternative asset in this study replicated. Outside of those exceptional windows, the risk-reward proposition was poor.

> **Verdict:** ETH was worth considering as a small, high-conviction allocation within a diversified portfolio, but not as a core holding. The volatility premium was not systematically compensated by superior risk-adjusted returns relative to BTC or the NASDAQ-100.

---

### 2. Objective Asset Quality Assessment

By conventional quantitative standards, ETH does not qualify as a high-quality asset over this period:

| Metric | ETH | BTC | NASDAQ-100 | Quality Threshold |
|--------|-----|-----|------------|-------------------|
| Sharpe Ratio | 0.17 | 0.29 | 0.52 | ≥ 0.50 considered acceptable |
| Sortino Ratio | 0.23 | 0.34 | 0.48 | ≥ 1.00 considered strong |
| Calmar Ratio | 0.23 | 0.30 | 0.44 | ≥ 1.00 considered strong |
| Max Drawdown | −77.0% | −73.0% | −33.0% | ≤ −30% is high-risk territory |

All four risk-adjusted metrics fall well below institutional thresholds. The Calmar ratio of 0.23 means that for every percentage point of historical peak-to-trough loss endured, only 0.23 percentage points of annualised return were delivered. On the Risk–Return scatter plot (Plot 9), ETH sits clearly **below the Capital Market Line** (Sharpe = 1.0), confirming that the asset undercompensates investors for the risk carried.

The rolling Sharpe chart (Plot 4) further illustrates this: the ratio exceeded 1.0 only during the 2023 recovery window and spent the majority of the period near zero or negative, including the entirety of 2022 and 2025. The monthly heatmap (Plot 2) reinforces the asymmetry — the single worst month (June 2022: −45.1%) wiped out roughly four months of an average positive month in a single stroke.

> **Verdict:** By standard quantitative criteria — Sharpe, Sortino, Calmar, and drawdown depth — ETH is not a high-quality asset in the institutional sense. It is a high-octane, cycle-dependent instrument whose outsized gains materialise only in specific windows of crypto market euphoria.

---

### 3. Maximum Drawdown and Recovery Time

The maximum drawdown of **−77.0%** was recorded in **June 2022**, the trough of a bear market that began from the November 2021 peak. This drawdown was driven by a confluence of macro shocks: Federal Reserve rate hikes, the Terra/LUNA ecosystem collapse, and cascading leverage unwinds across centralised exchanges.

Key drawdown statistics:
- **Drawdown onset:** November 2021 (ETH peak ~$4,800)
- **Trough reached:** June 2022 (ETH ~$1,050) — a −77% decline over ~7 months
- **Recovery to prior peak:** approximately Q1–Q2 2024 — a recovery period of **~18–20 months** from the trough
- **Total time spent underwater (below prior peak):** the majority of 2022, all of 2023, and into early 2024 — roughly **26 months** of the 60-month study period

For context, BTC's maximum drawdown was −73.0% (December 2022), and NASDAQ-100's was −33.0% (also December 2022), both synchronised with ETH's bear market, confirming macro-driven rather than ETH-specific causation. The multi-asset drawdown chart (Plot 10) shows all three assets entering drawdown simultaneously in 2022 and recovering across 2023–2024.

Additional secondary drawdowns of 20–40% were recorded in 2024–2025 (visible in Plot 5 and the monthly heatmap), highlighting that full peak-recovery does not preclude subsequent material losses.

> **Verdict:** An investor who entered at any 2021 high would have waited more than two full years to recover their capital — a timeline incompatible with capital-preservation mandates or short investment horizons.

---

### 4. Correlation with Macro Factors — DXY and Traditional Markets

**ETH vs. DXY (US Dollar):**
The Pearson correlation between ETH and DXY monthly returns is **ρ = −0.011**, with a p-value of **0.934** — statistically indistinguishable from zero at any conventional significance level. The OLS regression confirms this: β = −0.12 and R² = 0.0001, meaning the DXY explains virtually **0% of ETH's variance**. Despite the widely cited narrative that crypto assets benefit from dollar weakness, the data over 2021–2026 provides no statistical support for ETH as a USD hedge. The relationship is negligible in both magnitude and reliability.

**ETH vs. Bitcoin:**
The ETH–BTC full-period correlation is **ρ = 0.766 (p < 0.01)**, and the 12-month rolling correlation averaged **ρ = 0.862**, rarely dipping below 0.60 at any point in the study. This near-lockstep co-movement means that holding both ETH and BTC provides minimal diversification — an investor exposed to both is effectively holding a levered version of the same underlying crypto market cycle.

**ETH vs. NASDAQ-100:**
The ETH–NASDAQ-100 correlation is **ρ = 0.611 (p < 0.05)**, averaging 0.622 on a rolling 12-month basis. This moderate-to-strong positive relationship reflects ETH's growing identity as a **risk-on asset** that trades in sympathy with high-growth technology equities. The rolling correlation chart (Plot 12) shows this relationship was persistent and relatively stable throughout the period, suggesting a structural link rather than coincidental co-movement.

> **Verdict:** ETH is statistically decoupled from the US dollar — it provides no meaningful macro hedge. However, it is meaningfully correlated with both Bitcoin and technology equities, positioning it firmly within the risk-on complex. In macro sell-off environments, ETH amplifies rather than mitigates drawdowns.

---

### 5. Return Consistency — Durable Compounding vs. Volatility Spikes

Annual geometric returns across the five-year period reveal a deeply inconsistent return profile:

| Year | ETH | BTC | NASDAQ-100 | Commentary |
|------|-----|-----|------------|------------|
| 2021 | +208% | +44% | +29% | ETH leads all assets by a wide margin |
| 2022 | −68% | −64% | −33% | Synchronised crash; ETH deepest loss |
| 2023 | +91% | +155% | +54% | Recovery year; BTC significantly outpaces ETH |
| 2024 | +46% | +121% | +25% | Bull continuation; BTC again decisively ahead |
| 2025 | −11% | −6% | +20% | ETH negative while NASDAQ-100 gains |

Three structural patterns emerge from this data:

1. **ETH's CAGR is front-loaded:** The headline 18.0% CAGR is overwhelmingly a function of the 2021 explosion (+208%). Strip that year out and the 2022–2025 sub-period is essentially flat to negative in real terms.

2. **ETH underperformed BTC in the two most recent bull years:** In 2023 and 2024, BTC returned +155% and +121% respectively, while ETH delivered +91% and +46%. This suggests ETH lost relative strength within the crypto asset class during the most recent cycle.

3. **ETH decoupled negatively from the NASDAQ-100 in 2025:** While technology equities gained +20%, ETH declined −11%, pointing to potential structural headwinds specific to Ethereum rather than broad macro pressure.

The rolling Sharpe chart (Plot 4) confirms the episodic nature of ETH's returns: risk efficiency spikes sharply during brief bull windows and reverts to near-zero or negative for extended periods.

> **Verdict:** ETH's returns are not the product of consistent, durable compounding. They are driven by isolated, cycle-dependent volatility spikes — principally 2021 and portions of 2023. Investors who did not enter and exit within these specific windows materially underperformed relative to the headline CAGR.

---

### Overall Summary

Ethereum over 2021–2026 presents a paradox familiar to high-volatility assets: impressive raw returns that dissolve under risk-adjustment scrutiny.

| Dimension | Finding |
|-----------|---------|
| Absolute return | Competitive (+126% cumulative, 18.0% CAGR) |
| Risk-adjusted return | Poor — lowest Sharpe (0.17) among all benchmarks |
| Drawdown tolerance required | Extreme — −77% maximum, ~2-year recovery |
| Dollar hedge utility | None — statistically zero correlation with DXY |
| Diversification vs. BTC | Minimal — rolling ρ averaging 0.86 |
| Equity correlation | Moderate-strong — ρ = 0.61 vs. NASDAQ-100 |
| Return consistency | Low — CAGR driven by two exceptional bull years |

For a quantitatively rigorous portfolio, ETH is best understood as a **high-beta, cycle-dependent speculation** on the continued adoption of the Ethereum network. It is capable of extraordinary returns in favourable market regimes, but carries tail risk, long recovery horizons, and no macro-hedging properties that would justify a strategic allocation under conventional risk management frameworks. Its most appropriate role is as a **small, time-bounded, cyclically managed position** within a broader risk-on allocation — sized to reflect a maximum tolerable loss of 75–80% of the invested amount.

---

## Disclaimer

This project is for **educational and quantitative research purposes only**.
Nothing herein constitutes financial or investment advice.
Past performance of Ethereum does not guarantee future results.
Cryptocurrency investments carry substantial risk of total loss.
