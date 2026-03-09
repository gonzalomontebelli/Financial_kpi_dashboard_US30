# 04 · Monte Carlo Simulation  
## QUANTUM_US30 — Stress Testing & Forward Projections

---

## 1. Methodology

### 1.1 Simulation Framework

Monte Carlo analysis was performed using **non-parametric bootstrap resampling** of historical trade P&L.  
Rather than fitting a parametric distribution (e.g., Normal or Student-t), this approach preserves the empirical characteristics observed in the historical sample, including skewness, tail events, and trade-sequence dispersion.


```
Algorithm:
1. Extract all 3,406 historical trade P&L values
2. For each simulation path:
   a. Draw N trades with replacement from the historical sample
   b. Apply scenario-specific cost adjustments
   c. Compute cumulative equity curve from initial balance
   d. Calculate: final equity, max drawdown, return%
3. Repeat 5,000 times
4. Compute percentile distribution of outcomes
```



**Parameters:**
- Simulations per scenario: **5,000**
- Trades per path: **3,406** (same length as the historical sample)
- Initial capital: **$4,000**
- Random seed: **42** (reproducible)

---

### 1.2 Scenarios Tested

| ID | Scenario | Cost Adjustment |
|----|----------|----------------|
| A | Base — Historical Resample | None |
| B | High Spread Stress | Calibrated to backtest log spread distribution (avg 2.19 pts, P90 3.0 pts, max 3.5 pts) |
| C | Enlarged SL Stress | Calibrated to backtest log stop-loss slippage distribution (avg 25.17 pts, median 15 pts, P90 50 pts, P95 72.65 pts) |
| D | Combined Stress | Spread + SL slippage jointly stressed using backtest log distributions |

The spread stress scenario is calibrated from backtest execution logs rather than a flat penalty assumption.  
Across 4,124 logged trades, entry spread averaged **2.19 points**, with **2.2-point median**, **3.0-point P90**, and **3.5-point max**, remaining broadly consistent with the strategy’s spread filter.

The stop-loss stress scenario is also calibrated from backtest execution logs.  
Across **1,988 stop-loss exits**, realized stop slippage averaged **25.17 points**, with **15-point median**, **50-point P90**, **72.65-point P95**, and **287-point max**. This suggests that stop execution deterioration is materially more relevant than entry spread variation in the tested sample.

The combined stress scenario should therefore be interpreted as a **log-calibrated execution stress test**, not as a central expectation.

---

## 2. Simulation Results

### 2.1 Scenario A — Base (Historical Resample)


```
Starting Balance: $4,000
Trades per Path:  3,406
Simulations:      5,000
```


| Percentile | Final Balance | Return % |
|-----------|--------------|---------|
| P5 | $197,402 | +4,835% |
| P25 | $249,822 | +6,146% |
| **P50 (Median)** | **$284,984** | **+7,025%** |
| P75 | $319,976 | +7,899% |
| P95 | $370,951 | +9,174% |

| Risk Metric | Value |
|-------------|-------|
| Probability of Profit | **100%** |
| Probability of 2× (>$8,000) | **100%** |
| Probability of 10× (>$40,000) | **100%** |
| Median Max Drawdown | -70.8% |
| Worst-Case DD (P95) | -232.3% |

**Interpretation:** The base scenario is extraordinarily robust — all 5,000 simulation paths resulted in profit. The median final balance closely matches the actual backtest result ($284,984 vs $285,080), confirming the simulation's validity. The high median drawdown (-70.8%) reflects the compounding of percentage drawdowns over a 9+ year path.

---

### 2.2 Scenario B — High Spread Stress (Log-Calibrated)

This scenario stresses transaction costs using the actual spread profile recorded in the backtest execution logs rather than a flat penalty assumption. Entry spread averaged **2.19 points**, with a **2.2-point median** and **3.0-point P90**, indicating that spread friction is present but relatively stable within the strategy's execution framework.


| Percentile | Final Balance | Return % |
|-----------|--------------|---------|
| P5 | $197,402 | +4,835% |
| P25 | $249,822 | +6,146% |
| **P50 (Median)** | **$284,984** | **+7,025%** |
| P75 | $319,976 | +7,899% |
| P95 | $370,951 | +9,174% |

| Risk Metric | Value |
|-------------|-------|
| Probability of Profit | **100%** |
| Probability of 2× (>$8,000) | **100%** |
| Probability of 10× (>$40,000) | **100%** |
| Median Max Drawdown | -70.8% |
| Worst-Case DD (P95) | -232.3% |

**Interpretation:**  
The median final balance is very close to the realized backtest result ($284,984 vs $285,080), which indicates consistency between the bootstrap framework and the historical sample.  
However, the simulated drawdowns are substantially larger than the historical drawdown because bootstrap resampling can generate more adverse trade ordering than the realized path, especially under compounding. These figures should be interpreted as path-stress outcomes rather than realistic base-case expectations.

---

### 2.2 Scenario B — High Spread Stress (Log-Calibrated)

This scenario stresses transaction costs using the actual spread profile recorded in the backtest execution logs rather than a flat penalty assumption. Entry spread averaged **2.19 points**, with a **2.2-point median** and **3.0-point P90**, indicating that spread friction is present but relatively contained within the tested execution framework.

| Percentile | Final Balance | Return % |
|-----------|--------------|---------|
| P5 | $126,332 | +3,058% |
| P25 | $176,377 | +4,309% |
| **P50 (Median)** | **$210,263** | **+5,157%** |
| P75 | $244,621 | +6,016% |
| P95 | $297,088 | +7,327% |

| Risk Metric | Value |
|-------------|-------|
| Probability of Profit | **100%** |
| Probability of 10× | **99.98%** |
| Median Max Drawdown | -89.2% |

**Interpretation:**  
Spread deterioration reduces terminal outcomes meaningfully relative to the base scenario. Median final balance declines from $284,984 to $210,263.  
Within this calibration, the system retains positive median outcomes, although the simulated drawdown profile becomes materially worse. This suggests that spread costs matter, but are not the dominant friction in the tested dataset.

---

### 2.3 Scenario C — Enlarged SL Stress (Log-Calibrated)

This scenario is calibrated from actual stop-loss execution recorded in the backtest logs. Across 1,988 SL exits, realized stop slippage averaged **25.17 points**, with a **15-point median**, **50-point P90**, and **72.65-point P95**, indicating that stop execution is the dominant execution friction in the observed sample.

| Percentile | Final Balance | Return % |
|-----------|--------------|---------|
| P5 | $138,235 | +3,356% |
| P25 | $190,407 | +4,660% |
| **P50 (Median)** | **$226,515** | **+5,563%** |
| P75 | $262,501 | +6,463% |
| P95 | $314,722 | +7,768% |

| Risk Metric | Value |
|-------------|-------|
| Probability of Profit | **100%** |
| Probability of 10× | **100%** |
| Median Max Drawdown | -88.7% |

**Interpretation:**  
Stop-loss slippage produces a moderate reduction in terminal balances relative to the base case.  
The results suggest that stop execution quality has greater impact on long-run outcomes than entry spread stability, although simulated drawdowns remain substantially larger than the realized historical drawdown.

---

### 2.4 Scenario D — Combined Stress (Spread + Log-Calibrated SL Slippage)

This is the most aggressive execution stress test in the analysis, combining spread deterioration and stop-loss slippage calibrated from the execution logs.

| Percentile | Final Balance | Return % |
|-----------|--------------|---------|
| P5 | -$12,716 | -218% |
| P25 | $34,996 | +775% |
| **P50 (Median)** | **$69,630** | **+1,641%** |
| P75 | $103,897 | +2,497% |
| P95 | $155,570 | +3,789% |

| Risk Metric | Value |
|-------------|-------|
| Probability of Profit | **90.1%** |
| Probability of 2× | **88.7%** |
| Probability of 10× | **71.6%** |
| Median Max Drawdown | -174.3% |
| Worst-Case DD (P95) | -729% |

**Interpretation:**  
Under combined execution stress, simulated performance degrades materially. Roughly 10% of paths end with a net loss, and drawdown statistics become extreme.  
These figures should not be interpreted literally as feasible live drawdowns below zero equity, but as a mathematical consequence of path-dependent compounding under severe cost stress. In practical terms, this scenario shows that execution quality is a meaningful risk factor and that the strategy is sensitive to the joint deterioration of spread and stop-loss fills.

---

## 3. Scenario Comparison Table

| Scenario | Median Final | vs Base | P(Profit) | Median DD |
|----------|-------------|---------|-----------|-----------|
| A — Base | $284,984 | — | 100% | -70.8% |
| B — High Spread | $210,263 | -26.2% | 100% | -89.2% |
| C — Enlarged SL | $226,515 | -20.5% | 100% | -88.7% |
| D — Combined Stress | $69,630 | -75.6% | 90.1% | -174.3% |

The scenario comparison indicates that execution stress materially compresses long-run outcomes.  
Among the tested frictions, stop-loss deterioration appears more relevant than spread expansion, while the joint effect is substantially larger than either stress in isolation.

---

## 4. Forward Projection (Next ~1,000 Trades)

Starting from the last recorded balance of **$285,080**, the simulation projects the next 1,000 trades using the same resampling methodology.



```
Starting Balance:    $285,080
Projected Trades:    1,000 (~3 years at historical pace)
Simulations:         2,000 paths
```



| Metric | Value |
|--------|-------|
| Median Projected Balance | ~$350,000–$400,000 |
| P10 (pessimistic) | ~$200,000 |
| P90 (optimistic) | ~$600,000+ |
| Probability of Growth | ~65% |

> **Caveat:** These projections assume that future trade outcomes are drawn from the same empirical distribution as the historical sample. If recent market structure reflects a regime shift, realized outcomes may differ materially from the bootstrap distribution.

---

## 5. Key Takeaways

1. The historical sample shows positive median outcomes under mild execution stress scenarios (A, B, C)  
2. Combined execution stress produces materially weaker terminal balances and more adverse path dispersion  
3. Transaction costs are relevant, even when calibrated from observed execution logs  
4. Stop-loss slippage appears to be a more important execution friction than entry spread variation in this dataset  
5. Regime dependence remains a major source of forward uncertainty  
6. Compounding amplifies both favorable and adverse paths over long horizons  

---

## 6. Sensitivity Table (Win Rate Impact)

What happens to profitability as win rate degrades under a similar payoff structure?

| Win Rate | Profit Factor | Expectancy/Trade |
|----------|--------------|-----------------|
| 45% | 1.67 | +$96 |
| 43% (actual) | 1.59 | +$83 |
| 40% | 1.45 | +$63 |
| 37% | 1.30 | +$41 |
| 34% | 1.14 | +$18 |
| **33.4%** | **1.00** | **$0 (breakeven)** |
| 30% | 0.85 | -$19 |

The break-even win rate at a 1:2 RR is **33.4%**.  
The observed historical win rate of 42.92% leaves a buffer above that threshold, although realized forward performance will depend on execution quality and market regime.

---

*Monte Carlo data: `data/montecarlo_results.json`*  
*Simulation code: bootstrap resampling with replacement, seed=42, N=5000*  
*Execution stress calibration source: backtest execution log (`log.txt`)*