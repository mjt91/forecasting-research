---
title: "SOCK: Random Convolutional Features for Financial Time Series"
created: 2026-06-05
updated: 2026-06-05
type: concept
tags: [forecasting, time-series, neural-net, finance, arxiv]
sources: [raw/papers/2606.05138.md]
---

# SOCK: Random Convolutional Features for Financial Time Series

## Summary

Mueller et al. (2026) introduce SOCK (SOft Competing Kernels) — a fully differentiable random convolutional feature map for training generative models on financial time series. Prior approaches (ROCKET, Hydra) used random convolutional features for classification/regression but couldn't supervise generative models because the features are non-differentiable. SOCK resolves this by making the random kernels "soft" (differentiable), enabling gradient-based training of generators that match real and synthetic series in feature space. On small-sample financial datasets, SOCK consistently outperforms signature-based and diffusion baselines. The method also applies to two-sample hypothesis testing and time series classification.

## Key Findings

- **SOCK makes random convolutional features differentiable**: ROCKET/Hydra random kernels use hard argmax activations; SOCK replaces these with soft competing kernels that allow gradient flow — enabling adversarial training of generators.
- **Small-sample overfitting mitigated**: With only one historical path available, adversarial discriminators memorize training samples. Matching untrained SOCK features avoids this by using frozen random features rather than learned discriminators.
- **Outperforms signature and diffusion baselines**: Consistent gains across a wide range of small-sample financial datasets. Signature features can fail to capture relevant TS properties at tractable truncation depths — SOCK is more expressive.
- **Broad applicability**: Two-sample hypothesis testing and TS classification both benefit from SOCK features — not just generative training.

## Techniques

Applicable to Nixtla stack or similar production systems:

- **Synthetic data augmentation for scarce regimes**: SOCK-trained generators could augment training data for under-represented market regimes (crisis, low vol), similar to [[sbbts-schrodinger-bass-synthetic-ts]] but with a different feature matching objective.
- **Generative augmentation pipeline**: Could insert before training deep learning forecasters (N-BEATS, PatchTST) to increase effective sample size in low-data regimes.
- **Time series classification as preprocessing**: SOCK features as input to a classifier could improve regime detection — e.g., feeding SOCK feature vectors into a regime classifier rather than raw returns.
- **Two-sample testing for model validation**: Could use SOCK two-sample test to validate whether synthetic series from a generator are statistically indistinguishable from real series — useful for backtesting synthetic data pipelines.

## My Notes

The paper bridges two worlds: random feature methods (ROCKET, Hydra) from the time series classification literature, and generative modelling (Schrödinger Bridges, diffusion) from the generative literature. The key insight — that differentiable random features unlock adversarial training — is clean and compelling.

For production forecasting: the most actionable application is data augmentation. If you're building a forecaster for a market with limited history (emerging markets, new instruments), training a SOCK generator to produce synthetic paths could meaningfully improve model robustness. The comparison to [[sbbts-schrodinger-bass-synthetic-ts]] is interesting — both address small-sample financial TS generation, but SOCK uses adversarial feature matching while SBBTS uses Schrödinger-Bass bridges. Worth comparing both on the same dataset.

The cross-list (cs.LG + q-fin.ST) reflects the methodological novelty — this is as much a machine learning paper as a finance paper. Nixtla practitioners who work on neural forecasting methods should find this directly relevant.

## Links

- [[sbbts-schrodinger-bass-synthetic-ts]] — alternative approach to synthetic financial TS generation
- [[conformal-seasonal-pools]] — training-free probabilistic forecasting as alternative to generative approaches
- [[bayesian-dynamic-realized-volatility]] — Bayesian vol modelling context
- [arXiv:2606.05138](https://arxiv.org/abs/2606.05138)