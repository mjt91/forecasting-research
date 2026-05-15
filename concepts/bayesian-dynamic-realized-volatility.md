---
title: Bayesian Dynamic Modeling of Realized Volatility in Financial Asset Price Forecasting
created: 2026-05-15
updated: 2026-05-15
type: concept
tags: [forecasting, time-series, statistical, finance, arxiv]
sources: [raw/papers/2605.12099.md]
---

# Bayesian Dynamic Modeling of Realized Volatility

## Summary

Woitschig & West (2026) introduce a new class of **Bayesian dynamic models** for bivariate price-realized volatility time series. The core innovation is integrating a **dynamic gamma process** — adapted for realized volatility modeling — with traditional **Bayesian dynamic linear models (DLMs)** for asset prices. This enables joint modeling of volatility leverage effects and feedback dynamics that standard GARCH-type approaches miss.

## Key Findings

- **Volatility feedback modeling**: Using realized volatility proxies (from high-frequency intraday data) as conditioning variables in DLMs for prices/returns captures the well-known leverage effect (negative returns → increased volatility) in a principled Bayesian framework
- **Sequential filtering**: Conjugate-form Bayesian analysis extends naturally to sequential filtering and forecasting with negligible computational overhead — the dynamic gamma process stays in the exponential family
- **S&P sector ETF empirical study**: Multi-ETF validation shows meaningful improvements in return forecasting relative to standard models
- **Scalability**: The analytic structure enables scaling to higher dimensions for portfolio-level multivariate forecasting (decouple/recouple applications)

## Techniques

- **Dynamic gamma process** for stochastic volatility tracking
- **Bayesian DLMs** (Harrison & West framework) for price/return series
- **High-frequency intraday data** synthesis for realized volatility proxies
- **Conjugate Bayesian inference** for fast sequential updating
- Multi-step-ahead simulation-based forecasting

## My Notes

Mike West's group has a long track record of principled Bayesian dynamic modeling. The key practical insight here is that separating realized volatility (measured from intraday data) from the DLM price model lets you capture the asymmetric vol feedback that standard approaches like GARCH handle awkwardly — but in a fully probabilistic, coherent forecasting framework. For a production system, the conjugate form is a major advantage: no MCMC, no variational inference, just fast Kalman-like updates. The extension to "decouple/recouple" portfolio construction (Section 4) is worth reading carefully if you're doing anything multi-asset.

The computational simplicity is notable: "negligible extra computational cost" over a standard DLM means this could slot into an existing [[specialist-routing-volatility]] or regime-switching pipeline without major infrastructure changes.

**Tag for future reference**: Bayesian dynamic models, realized volatility, Mike West, conjugate inference.

## Links

- [[specialist-routing-volatility]] — regime-dependent approaches to volatility forecasting
- [[probabilistic-electricity-forecasting-evaluation]] — probabilistic forecast evaluation in finance-adjacent domains
- [arXiv:2605.12099](https://arxiv.org/abs/2605.12099)
