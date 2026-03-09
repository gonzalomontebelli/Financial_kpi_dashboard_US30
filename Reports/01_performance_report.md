# 01 · Full Performance Report  
## QUANTUM_US30 — Backtest 2017–2026

---

## 1. Executive Summary

The QUANTUM_US30 system generated historical growth from an initial capital of **$4,000** to **$285,080** over 9.17 years of backtesting on the US30 index (M5 timeframe). This corresponds to a **Compound Annual Growth Rate (CAGR) of 59.24%**, with a maximum drawdown of -19.40% and positive annual results across the tested calendar years.

The system combines two complementary intraday frameworks — a London-range breakout (Strat1: LONDON_1B1S) and a post-London range reversal (Strat2: RRL). Across the tested period, the combined logic generated 3,406 completed trades with a win rate of 42.92% and a Risk/Reward structure close to 1:2 (SL 61.5 pips / TP 122.5 pips).

These results reflect historical backtest performance under defined assumptions and should not be interpreted as forward-looking expectations.

---

## 2. Core Performance Metrics

### 2.1 Capital Growth

| Metric | Value |
|--------|-------|
| Starting Capital | $4,000.00 |
| Final Equity | $285,080.17 |
| Net Profit | $281,080.17 |
| Total Return | +7,027.00% |
| CAGR | 59.24% per year |
| Consecutive Profitable Years | 10 out of 10 |

Growth over time is materially influenced by compounded position sizing rather than structural changes in expectancy.

---

### 2.2 Trade Statistics

| Metric | Value |
|--------|-------|
| Total Trades | 3,406 |
| Winning Trades | 1,462 |
| Losing Trades | 1,944 |
| Win Rate | 42.92% |
| Gross Profit | $756,653.61 |
| Gross Loss | -$475,573.44 |
| Profit Factor | 1.591 |
| Expectancy per Trade | +$82.53 |

The system operates with a moderate win rate and relies primarily on asymmetric payoff distribution rather than directional accuracy.

---

### 2.3 Trade Quality

| Metric | Value |
|--------|-------|
| Average Winning Trade | +$517.55 |
| Average Losing Trade | -$244.64 |
| Win/Loss Ratio | 2.12 |
| Largest Single Win | +$9,460.17 |
| Largest Single Loss | -$5,147.10 |
| Average Trade Duration | ~124 minutes |

All positions are closed intraday under defined session rules.

---

## 3. Annual Performance — Positive Results Across Tested Years

| Year | Trades | Net P&L ($) | Win Rate (%) | Balance (EOY) |
|------|--------|-------------|--------------|---------------|
| 2017 | 358 | +769 | 50.6% | ~$4,769 |
| 2018 | 398 | +179 | 41.0% | ~$4,948 |
| 2019 | 370 | +1,160 | 44.1% | ~$6,108 |
| 2020 | 340 | +494 | 40.3% | ~$6,602 |
| 2021 | 362 | +2,406 | 46.4% | ~$9,008 |
| 2022 | 374 | +8,612 | 40.4% | ~$17,620 |
| 2023 | 397 | +25,351 | 41.1% | ~$42,971 |
| 2024 | 361 | +48,582 | 41.3% | ~$91,553 |
| 2025 | 374 | +154,488 | 41.4% | ~$246,041 |
| 2026* | 72 | +39,039 | 44.4% | $285,080 |

\*Jan–Mar only.

The increase in nominal returns in later years reflects percent-risk scaling rather than changes in trade-level expectancy. Win rate remains relatively stable across the full sample.

---

## 4. Expectancy Analysis

At a 42.92% win rate with ~1:2 RR, the observed expectancy per trade is:


```
E = (p_win × avg_win) - (p_loss × avg_loss)
  = (0.4292 × 517.55) - (0.5708 × 244.64)
  = 222.23 - 139.67
  = +$82.56 per trade

Theoretical minimum win rate at 1:2 RR = 33.4%
Actual win rate = 42.92% → 9.52 percentage point buffer
```


The theoretical break-even win rate at 1:2 RR is ~33.4%.  
The tested sample shows a margin above this threshold.

---

## 5. Monthly Return Distribution

Based on 111 monthly observations:

- Profitable months: ~65%  
- Flat months: ~5%  
- Losing months: ~30%  

Monthly outcomes vary materially, though the long-term distribution remains positive.

---

## 6. Trade Duration

| Metric | Value |
|--------|-------|
| Average Duration | 124.1 minutes |
| Median Duration | ~90 minutes |
| Max Duration | ~7 hours |

All trades are closed before the defined session cutoff (16:55 NY), avoiding overnight exposure.

---

## 7. Observed Strengths

1. Positive results across all tested calendar years  
2. Asymmetric payoff structure (avg win vs avg loss)  
3. Consistent expectancy across large sample size  
4. Intraday-only exposure  
5. Event filtering reduces exposure during high-impact releases  
6. Risk scaling framework maintains proportional exposure  

---

## 8. Key Risks & Limitations

1. Commission assumptions are simplified — real execution costs may differ  
2. Compounding increases nominal drawdowns as equity scales  
3. Max drawdown (-19.40%) exceeds typical prop firm risk limits  
4. Slippage and liquidity conditions vary across regimes  
5. Performance is regime-dependent and may degrade in prolonged range-bound environments  

---

*Data source: cTrader backtest export (US30, M5, Jan 2017 – Mar 2026)*  
*Raw equity data: `data/equity_curve.csv`*
