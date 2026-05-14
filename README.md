# Smart-Beta — Sector-Adjusted Alpha & Factor Analysis Framework

Python regression engine that estimates **sector-relative alphas** across S&P sectors using rolling OLS and factor-residual decomposition. Identifies above-sector-mean performers, quantifies sector tilt, and ranks single-name equities against sector-implied benchmarks.

> **Status:** core model implemented. Streamlit MVP in development.

## What it does

Decomposes single-stock returns into a sector-implied component and an idiosyncratic residual (α), producing per-name diagnostics useful for portfolio construction, factor screening, and sector-relative valuation:

- Rolling **OLS regression** of stock returns vs. sector ETF returns
- Estimation of **α, β, residual variance, R²** per name
- **Above-sector-mean alpha** universe selection
- Sector buckets covered: financials, energy, industrials, consumer staples, growth, mid-cap

## Stack

Python · NumPy · Pandas · statsmodels · IEX Cloud API · Streamlit (MVP)

## Repository structure

| File | Purpose |
|---|---|
| `app.py` | Streamlit entry point |
| `metodology.py` | Single-index regression core |
| `financials.py`, `energy.py`, `industrial.py`, `consumo.py`, `growth.py`, `midcap.py` | Sector-specific computations |
| `funtions.py` | Shared helpers |
| `cache.py` | Cached data layer |
| `*.csv` | Pre-computed alphas, betas, and ETF universe |

## Methodology

Single-index OLS following the Sharpe single-index model, generalized across sector ETFs. For each stock _i_ in sector _s_:

```
r_{i,t} = α_i + β_i · r_{s,t} + ε_{i,t}
```

A name with statistically significant **α > 0** and **R² > threshold** is flagged as a candidate above-sector outperformer. Sector tilt is quantified by deviation of β from the cross-sector mean.

## Author

**Leonardo Suárez Romero, PhD** — Quantitative Data Analyst.
[leoromero.dev](https://leoromero.dev) · [LinkedIn](https://linkedin.com/in/leonardo-suarez-romero)
