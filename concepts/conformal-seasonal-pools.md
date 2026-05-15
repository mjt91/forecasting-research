---
title: Training-Free Probabilistic Time-Series Forecasting with Conformal Seasonal Pools
created: 2026-05-15
updated: 2026-05-15
type: concept
tags: [forecasting, time-series, statistical, production, arxiv]
sources: [raw/papers/2605.03789.md]
---

# Conformal Seasonal Pools (CSP)

## Summary

Manokhin (2026) proposes **Conformal Seasonal Pools (CSP)**, a training-free probabilistic forecaster that combines same-season empirical draws with signed residual draws around a seasonal naive baseline. On six benchmark datasets, CSP-Adaptive achieves **0.89 empirical 95% coverage** vs DeepNPTS's 0.66 — a massive calibration gap — while running **500x faster** on CPU. The paper makes a strong argument: any probabilistic forecaster that can't achieve nominal coverage in safety- or decision-critical settings (finance, healthcare, energy) is not deployment-ready.

## Key Findings

- **Coverage failure is systemic**: DeepNPTS fails catastrophically in the worst 10% of windows — prediction intervals miss the entire multi-step trajectory simultaneously. Aggregate coverage metrics hide this.
- **Training-free beats learned**: CSP, with zero learned parameters, substantially outperforms a learned non-parametric approach. This is a direct challenge to the "more learning = better forecasts" assumption.
- **Decision-critical applications**: The paper explicitly calls out finance as a domain where coverage failures translate to regulatory capital failures.
- **500x speedup**: CSP runs on CPU in milliseconds vs hours for learned approaches.

## Techniques

- **Conformal prediction** framework for distribution-free uncertainty quantification
- **Seasonal naive** baseline forecast as the point predictor
- **Same-season empirical draws** pooled across historical periods
- **Signed residual draws** around the seasonal naive to preserve sign asymmetry
- **Adaptive pooling** across seasonal periods
- **Rolling-origin evaluation** with proper coverage diagnostics

## My Notes

This is an important methodological counter-balance to the deep learning TS forecasting literature. The core argument is correct and underappreciated: **coverage at the nominal level is non-negotiable** in production forecasting systems, and aggregate metrics like mean CRPS can completely hide catastrophic failure modes in the tails. The failure mode analysis — where in 10% of windows, *all* horizons miss simultaneously — is exactly the kind of systematic bug that slips through standard benchmarks.

For Marius's production forecasting stack, CSP is relevant as a **mandatory calibration baseline**: any learned model should be tested against CSP before deployment. The training-free property means it's trivial to add to an experiment pipeline as a comparison point. This directly relates to the evaluation philosophy in [[probabilistic-electricity-forecasting-evaluation]] which also critiques benchmark design.

The paper is also a useful citation for the principle that simpler models often outperform complex ones on calibration — relevant to the Nixtla stack where you might compare neuralforecast models against statistical baselines.

**Contrarian claim**: The paper argues learned models may be unnecessary for probabilistic forecasting. Given Marius's skepticism of pure DL hype in finance, this is worth keeping in mind.

## Links

- [[probabilistic-electricity-forecasting-evaluation]] — probabilistic forecast evaluation methodology
- [[llm-stock-forecasting-hedge-fund-review]] — learned models vs baselines in finance
- [arXiv:2605.03789](https://arxiv.org/abs/2605.03789)
