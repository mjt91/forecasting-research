---
title: "Probabilistic Electricity Price Forecasting Evaluation"
created: 2026-04-24
updated: 2026-04-24
type: concept
tags: [forecasting, time-series, probabilistic, finance, electricity, evaluation]
sources: [raw/papers/2604.19580.md]
---

# Probabilistic Electricity Price Forecasting Evaluation

## Summary

Hirsch & Ziel (2026) expose critical flaws in using battery storage arbitrage as a benchmark for evaluating probabilistic electricity price forecasts. Quantile-based trading strategies (QBTS) systematically misrepresent forecast quality because they ignore intertemporal dependence and create perverse incentives for dishonest probabilistic forecasting.

## Key Findings

### Flaws in Battery Trading as Evaluation Benchmark

1. **Incentive misalignment**: QBTS do not reward honest probabilistic forecasting — a forecaster can manipulate quantile predictions to maximize trading profit without improving the underlying predictive distribution.
2. **Intertemporal dependence ignored**: Electricity prices exhibit strong serial dependence (spreads, mean reversion, spike clustering). QBTS treat each interval independently, destroying information.
3. **Stochastic program superiority**: Framing battery optimization as a stochastic dynamic program with full predictive distributions (rather than quantile summaries) properly preserves intertemporal structure and produces better decisions.

### Practical Implications for Evaluation

- **Economic value ≠ statistical improvement**: Better statistical scores don't automatically translate to better economic decisions. The evaluation-practice gap matters enormously in production.
- **Risk attitudes matter**: For risk-averse operators, the uncertainty model used in the stochastic program affects outcomes — a point often ignored in simple point/quantile forecast comparisons.
- **German market evidence**: Case study on the German electricity market demonstrates the gap between statistical and economic evaluation.

## Techniques Applicable to Production Forecasting

- **Stochastic programming** for decision-based forecast evaluation (vs. statistical error metrics)
- **Full predictive distributions** (not just quantiles) for operational decision-making
- Rolling walk-forward evaluation with proper decision metrics, not just MSFE/MAE
- The insight generalizes beyond electricity: any time series where decisions depend on multi-step joint uncertainty (portfolio construction, risk limits, inventory) should use full distribution forecasts

## My Notes

As a finance data scientist running production forecasting systems: this is a sharp critique of how most teams benchmark. We routinely rank models by MSFE or CRPS on a holdout set and present those rankings to stakeholders as "this model is better." But if the downstream decision doesn't decompose into independent quantile trades, that ranking may be misleading.

The stochastic program framing is closer to how we'd actually use forecasts in a production system — but it's harder to benchmark. Worth noting that Nixtla's `mlforecast` + `statsforecast` give you point and probabilistic forecasts; the step from there to actual economic decision-quality measurement is non-trivial and often skipped.

The critique of QBTS also matters for anyone building trading strategies off probabilistic forecasts: naive quantile-following isn't the same as using the full distribution.

## Links

- [[probabilistic-forecasting]] — broader concept
- [[electricity-price-forecasting]] — related application domain
- [Nixtla mlforecast](https://nixtlaverse.nixtla.io/mlforecast/) — production TS forecasting framework
- [arXiv:2604.19580](https://arxiv.org/abs/2604.19580)
