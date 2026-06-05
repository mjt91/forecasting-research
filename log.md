---
title: Wiki Log
created: 2026-04-18
updated: 2026-06-05
type: meta
tags: [meta]
sources: []
---

# Wiki Log

> Chronological record of all wiki actions. Append-only.

## [2026-04-18] create | Wiki initialized
- Domain: Time series forecasting research
- Structure: SCHEMA.md, index.md, log.md, raw/papers/, raw/articles/
- Repo: github.com/mjt91/forecasting-research
- Cron: Weekly — arXiv q-fin.ST + stat.ML (forecasting OR time series)

## [2026-04-24] ingest | Weekly arXiv digest — Week of 2026-04-24
- Papers reviewed: 20 (10 q-fin.ST + 10 stat.ML, deduped)
- Papers kept: 4 (2604.19580, 2604.10402, 2604.09821, 2604.07159)
- Papers discarded: 16 (too niche, theoretical, or not finance TS)
- Raw pages created:
  - raw/papers/2604.19580.md
  - raw/papers/2604.10402.md
  - raw/papers/2604.09821.md
  - raw/papers/2604.07159.md
- Wiki pages created:
  - concepts/probabilistic-electricity-forecasting-evaluation.md
  - concepts/specialist-routing-volatility.md
  - concepts/global-persistence-local-residual-panel-forecasting.md
  - models/sbbts-schrodinger-bass-synthetic-ts.md
- Weekly digest: weekly/2026-W17.md

## [2026-05-01] ingest | Weekly arXiv digest — Week of 2026-05-01
- Papers reviewed: 20 (10 q-fin.ST + 10 stat.ML, deduped)
- Papers kept: 2 (2604.27696, 2604.22801)
- Papers discarded: 18 (pure CV/NLP, no TS component, no finance relevance, or already in wiki)
- Raw pages created:
  - raw/papers/2604.27696.md
  - raw/papers/2604.22801.md
- Wiki pages created:
  - concepts/forecast-reconciliation-foreco-toolbox.md
  - concepts/context-adversarial-stock-prediction.md
- Weekly digest: weekly/2026-W18.md

## [2026-05-08] ingest | Weekly arXiv digest — Week of 2026-05-08
- Papers reviewed: 5 (4 q-fin.ST this week + 1 neural-actuarial; broader stat.ML/cs.LG scan via arXiv search)
- Papers kept: 2 (2605.05211, 2605.06310)
- Papers discarded: 3 (2605.04004 intraday signals - not production TS forecasting; 2605.00196 theoretical distribution paper - no Nixtla connection; 2605.06438 longevity risk - niche)
- arXiv API rate-limited all week — used browser browsing to discover papers; Semantic Scholar also rate-limited
- Raw pages created:
  - raw/papers/2605.05211.md
  - raw/papers/2605.06310.md
- Wiki pages created:
  - concepts/llm-stock-forecasting-hedge-fund-review.md
  - concepts/dpr-dynamic-pattern-recalibration.md
- Weekly digest: weekly/2026-W19.md

## [2026-05-15] ingest | Weekly arXiv digest — Week of 2026-05-15
- Papers reviewed: 68 (deduped from 6 broad queries: time series forecasting, finance TS, stock price, volatility, probabilistic)
- Papers kept: 3 (2605.12099, 2605.03789, 2604.16988)
- Papers discarded: 65 (pure CV/NLP without TS component, general ML without finance/production relevance, or too theoretical)
- arXiv API: category filters (q-fin.ST, stat.ML, cs.LG) returned 0 results due to query parsing; used broader all-field queries instead
- Raw pages created:
  - raw/papers/2605.12099.md
  - raw/papers/2605.03789.md
  - raw/papers/2604.16988.md
- Wiki pages created:
  - concepts/bayesian-dynamic-realized-volatility.md
  - concepts/conformal-seasonal-pools.md
  - concepts/in-context-learning-regime-change.md
- Weekly digest: weekly/2026-W20.md

## [2026-05-29] ingest | Weekly arXiv digest — Week of 2026-05-29
- Papers reviewed: 12 (from q-fin.ST recent list + stat.ML recent list; arXiv API rate-limited all day)
- Papers kept: 3 (2605.29541, 2605.27848, 2605.27977)
- Papers discarded: 9 (pure CV/NLP, general ML without finance/production TS relevance, or low relevance to production forecasting)
- arXiv API: fully rate-limited ("Rate exceeded" persists for hours); all discovery via browser browsing of category list pages
- Papers kept理由:
  - 2605.29541: Copula-Weibull Markov change-point detection for volatility series; direct VIX COVID-19 application
  - 2605.27848: HMM+RL regime-aware portfolio allocation; 3-state BIC-selected; best Sharpe with interpretable discrete actions
  - 2605.27977: MLP vs CNN-GAF on bond index; fractional differencing key; CNN-GAF consistently fails — lesson for architecture selection
- Raw pages created:
  - raw/papers/2605.29541.md
  - raw/papers/2605.27848.md
  - raw/papers/2605.27977.md
- Wiki pages created:
  - concepts/copula-weibull-change-point.md
  - concepts/hmm-regime-rl-allocation.md
  - concepts/deep-learning-bond-index-forecasting.md
- Weekly digest: weekly/2026-W22.md

## [2026-06-05] ingest | Weekly arXiv digest — Week of 2026-06-05
- Papers reviewed: ~13 (browsed q-fin.ST recent list across 5 days; arXiv API fully rate-limited all day)
- Papers kept: 3 (2606.06190, 2606.05138, 2606.04153)
- Papers discarded: ~10 (crypto DRL pair trading too niche; life insurance surplus too actuarial; general ML papers without finance TS component)
- Raw pages created:
  - raw/papers/2606.06190.md
  - raw/papers/2606.05138.md
  - raw/papers/2606.04153.md
- Wiki pages created:
  - concepts/multi-scale-ms-garch.md
  - concepts/sock-random-convolutional-features.md
  - concepts/sign-magnitude-return-decomposition.md
- Weekly digest: weekly/2026-W23.md
