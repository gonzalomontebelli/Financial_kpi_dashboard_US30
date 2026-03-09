## Execution Frictions in Context — Daily Evidence

To better understand real execution impact, spread and slippage were analyzed alongside daily trading results using matched CSV and execution log data.

The table below aggregates daily outcomes showing:

- number of trades executed  
- daily win rate  
- daily PnL  
- average spread  
- realized slippage  

---

## Key Observations

### 1. Execution Frictions Were Not Deterministic

Across observed sessions:

- Several days showed **elevated slippage with positive PnL**
- Some losing days occurred under **typical execution conditions**
- No stable relationship was observed between execution friction and profitability

This suggests that results appear primarily driven by the underlying strategy logic rather than execution variability alone.

---

### 2. Real Examples (From Observed Sample)

Examples drawn from the dataset:

- **2026-02-03**
  - Trades: 3  
  - Slippage: ~28.7 pts  
  - Result: **strongly profitable**

- **2026-02-17**
  - Trades: 1  
  - Slippage: ~204 pts  
  - Result: **loss**

- **2026-02-27**
  - Trades: 1  
  - Slippage: ~47 pts  
  - Result: **profitable**

These examples indicate that large slippage values do not consistently determine outcomes.

---

### 3. Typical Execution Conditions

Across the observed period:

- Spread typically ranged between **1.6 and 2.2 pts**
- Slippage was most often between **15–50 pts**
- Extreme values occurred only sporadically

This is consistent with the broader execution profile measured across the full backtest sample.

---

## Interpretation

Execution frictions clearly exist and affect individual trades, but:

- They do not appear to explain overall system performance
- Their behavior is consistent with intraday index execution conditions
- Extreme slippage events appear as isolated tail occurrences rather than recurring conditions

While execution frictions are clearly present, their variability and occasional severity should be expected in intraday index trading environments, particularly during fast-moving sessions.

These results should be interpreted as descriptive of historical execution conditions rather than predictive of future performance.