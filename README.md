# Hyperliquid Trading vs Fear & Greed Index — Sentiment Impact Analysis

## Project Overview
This project analyzes Hyperliquid trade history and compares trader performance and behavior across **Fear vs Greed** market sentiment days using the Fear & Greed Index.

It answers:
1. Does performance (PnL, win rate, drawdown proxy) differ between Fear vs Greed days?
2. Do traders change behavior based on sentiment (trade frequency, trade size, long/short bias)?
3. Can traders be segmented into meaningful behavioral groups?
4. What actionable trading rules can be derived from the findings?

---

## Datasets Used
### Fear & Greed Index (`fear_greed_index.csv`)
Key columns:
- `timestamp`, `value`, `classification`, `date`

### Hyperliquid Trades (`historical_data.csv`)
Key columns:
- `Account`, `Coin`, `Side`
- `Execution Price`, `Size Tokens`, `Size USD`
- `Timestamp`, `Timestamp IST`
- `Closed PnL`, `Trade ID`

---
Methodology
Part A — Data Preparation

1. Loaded both datasets and documented:
  - number of rows/columns
  - missing values
  - duplicates
2. Converted timestamps into daily date format.
3. Aggregated Hyperliquid trade history to daily metrics.
4. Merged the daily trade metrics with daily sentiment (date as the join key).

Metrics Created (Daily)
From Hyperliquid:
- daily_pnl = sum of Closed PnL per day
- trades = number of trades per day
- avg_trade_size = average Size USD per day
- wins = count of trades with Closed PnL > 0
- win_rate = wins / trades
- long_short_ratio = Buy trades / Sell trades
From Fear & Greed:
- fear_value
- fear_class
- FG_group (Fear vs Greed)
Risk metric:
- drawdown proxy computed using cumulative PnL and rolling peak.

Analysis (Evidence-Based)
1) Does performance differ between Fear vs Greed days?
Performance was compared across sentiment groups using:
- average and median daily PnL
- win rate
- drawdown proxy
Output produced:
- tables comparing daily_pnl and win_rate by FG_group
- charts comparing PnL and win rate across sentiment regimes

2) Do traders change behavior based on sentiment?
Behavior changes were tested using:
- number of trades per day
- average trade size
- long/short ratio

Output produced:
- tables for trades/day and avg trade size by FG_group
- charts for trades/day, avg trade size, and long/short ratio by sentiment group

3) Trader Segmentation
Traders were segmented into 2–3 groups:
- Frequent vs infrequent traders (based on trades/day)
- High vs low risk traders (based on avg trade size)
- Consistent vs inconsistent traders (based on win rate)
This segmentation was used to interpret results more practically.

Key Insights (3)
Insight 1 — Performance differs by sentiment
Daily PnL and win rate show differences between Fear and Greed regimes.
Greed days generally show stronger performance, while Fear days show weaker stability.
Evidence: tables + charts comparing PnL and win rate by sentiment.

Insight 2 — Trading behavior shifts with sentiment
Trade frequency and trade sizing change across sentiment regimes.
Fear days tend to show more cautious behavior, while Greed days tend to show more aggressive participation.
Evidence: tables + charts comparing trades/day and avg trade size by sentiment.

Insight 3 — Long/Short bias shifts with sentiment
Long/short ratio tends to increase on Greed days (higher Buy bias), while Fear days become more balanced or Sell-heavy.
Evidence: long/short ratio tables + charts by sentiment.

Actionable Output (Strategy Rules)
Strategy Rule 1 — Sentiment-based risk control
Rule of thumb:
On Fear days: reduce leverage/position sizing and limit the number of trades.
On Greed days: allow normal sizing but enforce strict stop-loss rules.
Why: Fear regimes show weaker stability and higher downside risk.

Strategy Rule 2 — Sentiment-based directional bias
Rule of thumb:
On Greed days: allow a mild long bias (higher long/short ratio).
On Fear days: reduce long exposure and trade defensively.

Why: directional bias shifts with sentiment regimes.


### Option 1: Google Colab (Recommended)
1. Upload the notebook and both CSV files.
2. Install dependencies (if needed):
```bash
pip install pandas numpy matplotlib scikit-learn


