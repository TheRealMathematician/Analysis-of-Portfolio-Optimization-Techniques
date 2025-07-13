# Analysis-of-Portfolio-Optimization-Techniques
---

# 📈 Analysis of Portfolio Optimization Techniques

## 🎯 Background and Overview

This project rigorously evaluates **advanced portfolio optimization techniques**—including denoising, clustering, and backtesting—applied to a small, high-correlation portfolio of five major technology stocks:

* Apple (AAPL)
* Amazon (AMZN)
* Google (GOOGL)
* Microsoft (MSFT)
* Tesla (TSLA)

The objective is to measure how sophisticated covariance estimation and allocation methods improve (or fail to improve) risk-adjusted returns relative to the classic **Markowitz mean-variance framework**.

While prior research highlights the benefits of denoising and clustering in large portfolios, this study demonstrates the nuanced tradeoffs in smaller, less diversified universes.

> 💡 **Why it matters:** Even though the dataset is limited, this work provides a reproducible benchmark and foundation for scaling up to portfolios with **hundreds of assets**, where noise and estimation error become more severe.

---

## 🗂️ Data Structure Overview

### 🪙 Core Datasets

* **Price Data:**

  * Daily adjusted closing prices for the 5 tech stocks
  * Source: Yahoo Finance
  * Period: Jan 2018 – Jun 2019

* **Returns Matrix:**

  * Log returns computed from adjusted prices

* **Covariance and Correlation Matrices:**

  * Raw (sample) covariance estimates
  * Denoised versions (Targeted Shrinkage, Residual Eigenvalue)

* **Clusters:**

  * Hierarchical clusters created with NCO (Nested Cluster Optimization)

* **Backtest Splits:**

  * 2018 training period
  * Early 2019 and mid-2019 out-of-sample evaluation

---

## 🧭 Executive Summary

### 🔍 Key Findings

1. **Denoising Performance:**

   * **Targeted Shrinkage**: Reduced estimation noise and delivered **highest Sharpe ratio in early 2019 (4.74)** but sometimes oversimplified covariance structure, penalizing adaptability later on.
   * **Constant Residual Eigenvalue**: Preserved more weak signals but led to **higher portfolio volatility** and underperformance during stable markets.

2. **Clustering Performance:**

   * NCO grouped assets effectively (excluding TSLA) and yielded strong results, especially in mid-2019 when relative relationships shifted.
   * Outperformed all other methods in later out-of-sample periods, demonstrating adaptability.

3. **Backtesting Results:**

   | Period        | Best Strategy        | Sharpe Ratio |
   | ------------- | -------------------- | ------------ |
   | 2018 Training | Markowitz (Baseline) | 0.823        |
   | Early 2019    | Targeted Shrinkage   | 4.74         |
   | Mid-2019      | NCO Clustering       | *Best*       |

4. **Observations:**

   * **Asset Homogeneity:** With only five correlated stocks, sophisticated techniques added **marginal incremental gains**.
   * **Stable Market Regime:** No major volatility spikes or crashes reduced the impact of covariance adjustments.
   * **Metric Sensitivity:** Sharpe, Sortino, and drawdown-based evaluations did **not** always agree on the “best” strategy, emphasizing the need to align metrics with investor objectives.

---

## 🧠 Insights Deep Dive

### 📊 Denoising Techniques

* **Targeted Shrinkage:**

  * Capped small eigenvalues to stabilize estimates.
  * Reduced variance but occasionally erased subtle cross-asset relationships.

* **Constant Residual Eigenvalue:**

  * Averaged noise eigenvalues instead of nullifying them.
  * Retained more structure but produced **higher drawdowns** during flat periods.

### 🧬 Clustering with NCO

* Grouped AAPL, AMZN, GOOGL, and MSFT together.
* TSLA often treated as its own cluster due to idiosyncratic volatility.
* **Strengths:** Improved performance in mid-2019 as relative correlations drifted.
* **Weaknesses:** Less effective in highly stable or trending environments.

### 🧪 Backtesting & Validation

* Rolling window backtests confirmed **consistent relative rankings** across rebalancing periods.
* Sharpe ratio spikes in early 2019 reflected strong tech momentum.
* NCO showed higher adaptability over time, while shrinkage worked better during trending markets.

---

## 🛡️ Final Recommendations

### 🛠️ Implementation Strategy

* **For Small Portfolios (<10 assets):**

  * Simpler mean-variance or basic shrinkage methods likely sufficient.
  * Avoid over-engineering covariance estimators.

* **For Larger Portfolios (>30 assets):**

  * Denoising and clustering become **increasingly critical**.
  * Helps manage estimation error, stabilize turnover, and improve out-of-sample performance.

* **Dynamic Markets:**

  * Use **rolling re-optimization** (monthly or quarterly) instead of static allocations.

## 🚀 Future Enhancements

✅ **Expand Universe:** Add 50–200 stocks from diverse sectors to better showcase the power of denoising and clustering.

✅ **Dynamic Clustering:** Implement adaptive clustering that evolves as correlation structures change.

✅ **Factor Models:** Incorporate style or macro factors to improve covariance estimation.

✅ **Machine Learning:** Test Autoencoders or Graph Neural Networks to model hidden relationships.

✅ **Interactive Dashboard:** Build a **Streamlit** or **Dash** app to visualize portfolio composition, risk metrics, and scenario analysis.

✅ **Live Data Integration:** Connect to real-time data pipelines (e.g., IEX Cloud) for live backtesting.





