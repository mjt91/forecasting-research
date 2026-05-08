---
title: LLM Stock Forecasting - Hedge-Fund Review
created: 2026-05-08
updated: 2026-05-08
type: concept
tags: [llm, nlp, finance, stock-prediction, production, survey]
sources: [raw/papers/2605.05211.md]
---

# LLM Stock Forecasting — Hedge-Fund Review

## Summary

A practitioner-focused review paper (accepted at IEEE CAIT 2026) surveying LLM applications in quantitative finance for stock price forecasting. Unlike most academic papers that trumpet performance gains, this paper foregrounds **failure modes and practical pitfalls** — making it unusually valuable for someone building production systems.

## Key Findings

### Failure Modes Catalogued
1. **Sentiment fragility**: LLMs for sentiment extraction from financial news/social media are brittle to headline rewording, source differences, and temporal drift in language
2. **Dataset and horizon mismatch**: Many papers train on data that wouldn't be available at inference time; look-ahead bias sneaks in via non-causal feature engineering
3. **Evaluation metric misuse**: Sharpe ratios reported without transaction costs; accuracy metrics on smoothed/high-frequency data that don't reflect real trading P&L
4. **Data leakage**: Particularly in earnings-call analysis — transcript timing vs. announcement timing creates subtle look-ahead
5. **Illiquidity premia ignored**: Many signals only work on liquid names; transaction costs destroy alpha on illiquid small-caps
6. **Limits of predictability**: The paper acknowledges fundamental limits — even with perfect sentiment, stock prices are largely unpredictable at short horizons

### What Actually Works (with caveats)
- Extracting **earnings surprises** from transcripts (quantifiable, bounded noise)
- **Sector rotation** based on macro news themes (signal is slow-moving, more robust)
- **Options flow** integration as a sentiment proxy (institutional-grade data required)

### Multi-Agent Trading Systems
The paper reviews multi-agent LLM architectures for trading — agents specialized in different tasks (sentiment, fundamentals, technicals) coordinated by a meta-agent. The authors are skeptical: coordination overhead, latency, and failure propagation make these fragile in live trading.

## Techniques Relevant to Nixtla Stack / Production

- The criticism of **evaluation metrics** applies equally to any forecasting system — always report probabilistic metrics (CRPS, quantile loss) alongside point forecasts, and always include transaction costs
- **Regime conditioning**: The paper implicitly shows that LLMs fail during regime transitions — this connects to the [[specialist-routing-volatility]] approach already in the wiki
- For production systems using [[context-adversarial-stock-prediction]], the LLM sentiment features could be added as exogenous regressors in `neuralforecast`

## My Notes

As someone skeptical of pure DL hype in finance TS: this paper validates that skepticism but in a nuanced way. The failure modes aren't that LLMs don't work — it's that the **evaluation standards in the literature are garbage**. A hedge fund manager writing this is essentially saying: "we've tried these things for real and here's what actually breaks."

For production forecasting, the most actionable insight is the **evaluation rigor** point: if you're benchmarking a new model, you need walk-forward out-of-sample validation, transaction cost modeling, and multiple time periods including stress regimes.

The multi-agent architecture section is the most speculative — not actionable yet.

## Links

- [[specialist-routing-volatility]] — regime-dependent approach that addresses one of the failure modes
- [[context-adversarial-stock-prediction]] — adversarial training for distribution robustness
- [arXiv:2605.05211](https://arxiv.org/abs/2605.05211)