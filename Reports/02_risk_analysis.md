# 02 · Risk Analysis  
## QUANTUM_US30 — Drawdown, Ratios & Risk Profile

---

## 1. Drawdown Analysis

### 1.1 Maximum Drawdown

| Metric | Value |
|--------|-------|
| Max Drawdown (%) | -19.40% |
| Max Drawdown (USD) | -$26,521.08 |
| Drawdown Basis | Peak equity to trough equity |

The maximum drawdown observed in the tested period was **-19.40%**, measured from peak to trough equity.  
This level exceeds the limits of most prop firm risk frameworks (typically 10–15%), which is an important constraint for forward deployment under funded-account structures.

---

### 1.2 Drawdown Interpretation

The largest drawdown occurs in the later part of the sample (2024–2025), when equity and position sizing increase under the percent-risk model. As balance scales, identical percentage losses translate into materially larger nominal drawdowns.

**Observed patterns across the sample:**

- 2017–2023: Gradual equity growth with relatively shallow temporary drawdowns  
- 2024: First sustained adverse sequence; lower win rate and reduced expectancy  
- 2025: Extended losing phase; drawdown deepens before recovery  

These observations are consistent with compounding exposure and regime variation rather than structural deterioration of trade-level performance.

---

## 2. Risk-Adjusted Return Ratios

### 2.1 Sharpe Ratio

```
Sharpe = (Daily Mean P&L / Daily Std Dev P&L) × √252
       = 1.77
```


| Benchmark (reference) | Sharpe |
|-----------------------|--------|
| S&P 500 (long-term avg) | ~0.50 |
| Institutional multi-strategy range | ~1.0–2.0 |
| QUANTUM_US30 | 1.77 |

A Sharpe of 1.77 indicates strong risk-adjusted returns within the tested sample.  
Interpretation should remain conditional on assumptions and time period selection.

---

### 2.2 Sortino Ratio

```
Sortino = (Daily Mean P&L / Downside Deviation) × √252
        = 3.14
```


The Sortino ratio exceeds the Sharpe ratio, suggesting that variability is more concentrated on the upside than downside.

| Ratio | Value |
|-------|-------|
| Sharpe | 1.77 |
| Sortino | 3.14 |
| Sortino / Sharpe | 1.77 |

---

### 2.3 Calmar Ratio

```
Calmar = CAGR / |Max Drawdown|
       = 59.24% / 19.40%
       = 3.05
```

A Calmar ratio above 3 reflects strong historical return relative to drawdown in the tested sample, though future paths may differ materially.

---

## 3. Consecutive Trade Analysis

### 3.1 Win/Loss Streaks

| Metric | Value |
|--------|-------|
| Max Consecutive Wins | 15 |
| Max Consecutive Losses | 17 |
| Avg Consecutive Wins | ~3.2 |
| Avg Consecutive Losses | ~4.1 |

The observed maximum losing streak was **17 consecutive trades**.  
At a fixed 1% risk per trade, this implies a theoretical drawdown of approximately:
:

```
(1 - 0.01)^17 = 0.8429 → ~15.7% drawdown from a purely losing streak
```


Under percent-risk compounding, realized drawdowns depend on the equity level at the time of the streak.

---

### 3.2 Risk of Ruin (Theoretical Approximation)

Using a simplified Kelly-based framework:

```
f* = (p/a) - (q/b)
   = (0.4292/61.5) - (0.5708/122.5)
   = 0.00698 - 0.00466
   = 0.00232 (0.23% Kelly fraction)

Full Kelly = 0.23%
Half Kelly = 0.12%
```


This suggests relatively conservative sizing relative to full Kelly under tested assumptions.  
Actual risk-of-ruin depends heavily on execution conditions and regime variation.

---

## 4. Volatility Profile

### 4.1 Daily P&L Distribution

Based on daily aggregated P&L:

- Average daily P&L: ~+$83 per active trading day  
- Estimated daily standard deviation: ~+$1,200  
- Peak daily gain: ~+$9,000 (large wins during high-volatility periods)  
- Peak daily loss: ~-$5,000 (observed during adverse regimes)

These values reflect compounding exposure rather than fixed-risk nominal levels.

---

### 4.2 Monthly Return Distribution

Across 111 observed months:

- Profitable months: ~65%  
- Flat months: ~5%  
- Losing months: ~30%  

Monthly dispersion remains material despite positive long-term expectancy.

---

## 5. Regime Analysis

### 5.1 Performance by Market Regime

| Period | Market Condition | System P&L | Notes |
|--------|-----------------|-----------|-------|
| 2017–2019 | Low-vol bull market | +$2,108 | Smaller exposure, moderate edge |
| 2020 | COVID volatility | +$494 | Event filtering limited exposure |
| 2021 | Post-COVID trend | +$2,406 | Favorable directional structure |
| 2022 | Rate hike cycle | +$8,612 | Strong trending environment |
| 2023 | Sustained momentum | +$13,990 | Continued compounding growth |
| 2024–2026 | Range-heavy regime | -$63,290 | Reduced breakout efficiency |

---

### 5.2 Regime Sensitivity Interpretation

The strategy exhibits characteristics consistent with momentum and breakout systems, performing more consistently in trending environments and showing weaker results during mean-reverting regimes.

Future robustness may benefit from additional regime classification filters (e.g., volatility expansion metrics or trend strength thresholds).

---

## 6. Key Risk Parameters (Configuration Summary)

| Parameter | Value | Purpose |
|-----------|-------|---------|
| Max Daily Loss | 5% of daily balance | Hard stop — halts trading |
| Max Total Drawdown | 35% of initial | Hard termination rule |
| Warning Threshold | -10% total PnL | Monitoring trigger |
| Position Close Threshold | -35% | Emergency close logic |
| Drawdown Risk Scaling | >12% from peak | Risk reduced by 50% |
| Forced Close Time | 16:55 NY | Avoid overnight exposure |

---

*Data source: `data/summary_stats.json` · Equity series: `data/equity_curve.csv`*