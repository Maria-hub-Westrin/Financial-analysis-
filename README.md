## License
MIT © 2025 Maria Westrin

# Portfolio Risk Report — Transaction-to-Report Pipeline (Python)

A reproducible, bank-style analytics pipeline that goes from **raw transaction rows (BUY/SELL/DIVIDEND)** → **clean panel data** → **risk metrics + exposures** → **shareable HTML report**.

## Why this project (business value)
This project demonstrates an end-to-end workflow a data analyst/quant analyst would deliver:
- Data quality checks & validation (sanity checks, duplicates, missingness)
- Position building from transactions (signed volume/value, cumulative holdings)
- Daily portfolio panel construction (price/position/market value/exposure)
- Risk reporting (VaR, volatility, drawdown) + segment analyses
- Professional artifacts: **HTML report + figures + CSV tables**

## Key outputs (what recruiters should open first)
- **HTML report:** `report/portfolio_risk_report.html`
- **Figures:** `report/figures/*.png`
- **Tables:** `report/*.csv`

> Tip: add 1–2 screenshots from the HTML report into `assets/` and show them here.

## What the notebook does (high level)
### 1) Data ingestion & schema checks
- Reads `financial_raw_data.csv`
- Type casting for `date` and `timestamp`
- Overview table of dtypes, missingness, and basic stats

### 2) Data quality & consistency validation
- Duplicate checks (`transaction_id`)
- Consistency check: `price_per_share * volume ≈ transaction_value`
- Flags relative error and inspects worst rows

### 3) Build positions from transactions
- Signed volume/value (BUY = +, SELL = −)
- Instrument key primarily from `ticker_symbol` (fallbacks exist)
- Cumulative `position_units` per instrument over time

### 4) Build daily panel
- Daily snapshot per instrument
- Daily price series from last trade per day + forward-fill
- Returns computed from price (and optional comparison vs `daily_return` if present)

### 5) Portfolio return (robust definition)
- Computes portfolio return via **P&L / Gross Exposure**:
  \[
  r_t = \frac{\sum_i pos_{t-1,i}(P_{t,i}-P_{t-1,i})}{\sum_i |pos_{t-1,i}P_{t-1,i}|}
  \]
- Stable even if net exposure is near zero (gross-based denominator)

### 6) Risk reporting
- Historical **VaR 95%** (daily)
- Daily + annualized volatility
- Max drawdown on equity curve
- Exposures by sector and risk rating
- Optional signal check: `analyst_rating(t)` → `next-day return(t+1)` and robust regression outputs (HC3)

## Data requirements
This repo **does not need to publish your private dataset**. The notebook expects a CSV with transaction rows.

### Required columns (minimum)
- `transaction_id`
- `date`, `timestamp`
- `ticker_symbol` (or equivalent identifier)
- `transaction_type` (BUY/SELL/DIVIDEND)
- `price_per_share`, `volume`, `transaction_value`
- `currency`

### Optional (used for richer analyses/plots/tables)
- `company_name`, `sector`
- `risk_rating`, `liquidity_score`, `spread_pct`
- `analyst_rating`
- `daily_return` (if present, used for QC comparison)

## Reproducibility (how to run)
### Option A — Notebook (recommended)
1. Open `Financial_Analysis.ipynb` (or `financial_analysis_maria_westrin.ipynb`)
2. Restart Kernel → Run All
3. Open `report/portfolio_risk_report.html`

### Option B — From terminal (WSL/macOS/Linux)
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter notebook
