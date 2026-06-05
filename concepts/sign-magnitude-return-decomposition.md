---
title: "Sign-Magnitude Return Decomposition"
created: 2026-06-05
updated: 2026-06-05
type: concept
tags: [forecasting, time-series, statistical, finance, arxiv]
sources: [raw/papers/2606.04153.md]
---

# Sign-Magnitude Return Decomposition

## Summary

Brou & Luger (2026) propose a new approach to modelling financial returns by decomposing them into sign and magnitude (absolute value) components, with magnitude closely related to volatility. The joint distribution for expected returns is constructed in two stages: first model the marginal distribution of magnitude, then model the distribution of sign conditional on the contemporaneous magnitude. This decomposition captures nonlinear predictability in return dynamics that standard linear regressions miss. Out-of-sample evaluation on monthly U.S. stock market excess returns shows substantial statistical and economic gains over linear regression and complete subset regression, with competitive performance against copula-based return decomposition methods.

## Key Findings

- **Return decomposition R = sign × |R| separates vol from direction**: Modelling magnitude (|R|, related to volatility) and sign (direction) separately captures the insight that volatility contains information about return direction — high vol periods tend to have more negative skewness.
- **Conditional sign distribution captures asymmetry**: The conditional distribution of sign given magnitude captures asymmetric return dynamics (e.g., large magnitude days tend to be more negative than positive).
- **Outperforms linear benchmarks**: Substantial gains over linear regression and complete subset regression on monthly US stock excess returns. Competitive with copula-based decomposition methods.
- **Published in Journal of Banking and Finance**: Accepted manuscript — stronger evidence quality than typical arXiv preprints.

## Techniques

Applicable to Nixtla stack or similar production systems:

- **Volatility-informed directional forecasts**: Use magnitude forecasts (from GARCH-type models) to condition sign probability estimates — a principled way to combine vol and direction predictions.
- **Regime-dependent return distributions**: The sign-magnitude decomposition could inform regime-specific return distributions — in high-vol regimes, the conditional sign distribution shifts toward more negative outcomes.
- **Nonlinear return predictability**: Captures nonlinear patterns that linear regressions miss — useful for features in ML-based return forecasting models.
- **Copula alternative with fewer parameters**: If copula-based methods are too complex or computationally expensive, the sign-magnitude decomposition provides a simpler alternative with competitive performance.

## My Notes

The paper formalizes an intuition that practitioners have used informally: volatility is a signal about return direction. The two-stage modelling approach (magnitude first, then sign conditioned on magnitude) is clean and interpretable — you can inspect each stage separately.

For production systems: the most actionable takeaway is the conditional sign distribution. If you're forecasting returns (rather than just vol), feeding vol estimates into a sign model could improve directional accuracy. This is particularly relevant for risk management — tail events tend to be negative, and the sign-magnitude decomposition captures this asymmetry explicitly.

The comparison to copula-based methods is important: copulas are theoretically elegant but computationally complex for large-scale production systems. The sign-magnitude decomposition achieves competitive performance with a simpler framework — worth benchmarking against copula approaches in our context.

The Journal of Banking and Finance publication is a strong signal of quality — this isn't a throwaway arXiv preprint. The methodology is solid enough to consider for production evaluation.

## Links

- [[copula-weibull-change-point]] — copula-based methods for financial time series
- [[bayesian-dynamic-realized-volatility]] — Bayesian vol modelling that could feed into sign-magnitude decomposition
- [[hmm-regime-rl-allocation]] — regime-aware approach that could use sign-magnitude conditioned distributions
- [arXiv:2606.04153](https://arxiv.org/abs/2606.04153)