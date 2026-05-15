---
title: In-Context Learning Under Regime Change
created: 2026-05-15
updated: 2026-05-15
type: concept
tags: [forecasting, time-series, transformer, neural-net, finance, arxiv]
sources: [raw/papers/2604.16988.md]
---

# In-Context Learning Under Regime Change

## Summary

Dudley, Bi, Liu & Oymak (2026) formalize how transformer-based foundation models handle **regime shifts** via in-context learning. They frame regime change detection as an **in-context change-point detection problem** and prove that transformers can learn optimal policies. Empirically, incorporating changepoint knowledge into pretrained models improves performance on financial volatility forecasting around FOMC announcements without retraining.

## Key Findings

- **Regime change is fundamental**: Non-stationary sequences with unknown change points are the norm in finance (FOMC announcements, crisis periods, policy regime changes). Standard ICL breaks down here.
- **Transformers can learn change-point detection**: The authors prove that optimal in-context change-point detection is learnable, with complexity scaling by information available about changepoint location.
- **No-retraining adaptation**: Encoding explicit changepoint knowledge into pretrained foundation models improves volatility forecasting around FOMC announcements — without fine-tuning.
- **Practical applicability**: The approach extends to real-world financial problems beyond synthetic experiments.

## Techniques

- **In-context learning (ICL)** formalization as sequential decision making
- **Change-point detection** in non-stationary environments
- **Transformer architecture** as in-context learner
- **Linear dynamical systems** and **linear regression** as testbeds with known optimal solutions
- **Pretrained foundation model** adaptation without retraining
- **FOMC announcement** as real-world regime change test case

## My Notes

This paper directly addresses a key practical failure mode of transformer-based TS models: **they assume stationarity**, but financial time series are full of regime changes. The formal proof that transformers can learn change-point detection is reassuring, but the practical contribution is the FOMC result — showing that explicit changepoint encoding can boost pretrained models without any fine-tuning.

For production finance forecasting, this is relevant to the problem of **regime-aware forecasting**. If you're running a transformer-based model on financial data, you need a regime detection layer upstream. This paper gives theoretical grounding for why that matters and a practical approach for incorporating it. Related to [[specialist-routing-volatility]] which uses routing based on market regime.

The no-retraining result is particularly interesting: it suggests you could deploy a single pretrained model and handle regime changes through prompt-like context modification rather than full retraining or fine-tuning. For MLflow-based experiment tracking, this means keeping separate "regime-aware" evaluations rather than a single model.

**Practical takeaway**: When backtesting a TS forecasting model on financial data, test it specifically around known regime-change events (FOMC, earnings, etc.) and measure whether it detects and adapts to the shift.

## Links

- [[specialist-routing-volatility]] — regime-dependent specialist routing for volatility
- [[llm-stock-forecasting-hedge-fund-review]] — transformer models in finance production
- [arXiv:2604.16988](https://arxiv.org/abs/2604.16988)
