---
title: "Multi-Scale Markov Switching GARCH"
created: 2026-06-05
updated: 2026-06-05
type: concept
tags: [forecasting, time-series, statistical, finance, arxiv]
sources: [raw/papers/2606.06190.md]
---

# Multi-Scale Markov Switching GARCH

## Summary

Chaudhary (2026) proposes a triple-timeframe Markov-Switching GARCH framework that detects volatility regimes in EUR/USD across daily, 4-hour, and hourly horizons simultaneously. Rather than forcing a single-regime GARCH to capture non-stationary volatility, the method decomposes regime dynamics into macro (daily), meso (4H), and micro (1H) components, each modelled independently via AR(1)-MS-GARCH. Regime probabilities from each timeframe are combined via outer product into a 27-state cross-scale probability tensor. Filardo-style time-varying transition probabilities (TVTP) let regime switching respond to composite stress indicators at shorter horizons. The approach outperforms a conventional GARCH benchmark on out-of-sample volatility forecasting using EUR/USD data from 2015–2025.

## Key Findings

- **Multi-timescale regime structure is real and exploitable**: Statistically distinct Calm, Turbulent, and Crisis regimes emerge at each timescale. Modelling them separately provides more informative representation than single-regime GARCH.
- **27-state cross-scale tensor captures cross-timescale dependence**: Outer product of per-scale regime probabilities creates a rich state space that captures regime co-occurrence patterns (e.g., macro-crisis + micro-calm vs. macro-calm + micro-crisis).
- **TVTP improves short-horizon regime detection**: Filardo-style time-varying transition probabilities let the model adapt to market stress conditions rather than assuming time-invariant regime dynamics.
- **Out-of-sample vol forecasting superiority**: Triple MS-GARCH consistently beats conventional GARCH on holdout metrics — meaningful for production vol forecasting systems.

## Techniques

Applicable to Nixtla stack or similar production systems:

- **Volatility regime detection for risk management**: MS-GARCH can be used to construct regime-conditioned volatility forecasts — different forecast multipliers for Calm vs. Turbulent vs. Crisis regimes.
- **Multi-timescale signal combination**: The outer-product probability tensor approach is a template for combining signals from different forecast horizons. Could be adapted to combine daily/weekly/monthly forecasts in hierarchical reconciliation.
- **TVTP for adaptive model selection**: Filardo-style TVTP is a principled way to make transition probabilities data-dependent — could inform when to switch between GARCH variants in a production system.
- **Regime-conditioned risk limits**: The Calm/Turbulent/Crisis regime labels could drive dynamic position sizing or risk limits in a systematic trading workflow.

## My Notes

The 27-state tensor is conceptually elegant but could be sparse in practice — with only 3 regimes per scale, many of the 27 states may have negligible probability. Worth checking whether a reduced-state subset captures most of the predictive power. The TVTP approach is well-established in the econometrics literature (Filardo 1994) but rarely implemented in production. If the computational overhead is manageable, TVTP-MS-GARCH could be a strong upgrade to standard MS-GARCH for intraday vol forecasting.

The EUR/USD focus is reasonable but limited — would want to validate on other pairs (USD/JPY, GBP/USD) and possibly equity indices (SPX) before building a production system around it. The 2015–2025 training window includes COVID, which is good for crisis regime coverage.

## Links

- [[hmm-regime-rl-allocation]] — related regime-detection approach with HMM for portfolio allocation
- [[bayesian-dynamic-realized-volatility]] — Bayesian approach to realized volatility modelling
- [[specialist-routing-volatility]] — regime-dependent specialist routing for vol forecasting
- [arXiv:2606.06190](https://arxiv.org/abs/2606.06190)