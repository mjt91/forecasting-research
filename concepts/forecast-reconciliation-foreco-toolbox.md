---
title: "FoReco and FoRecoML: Forecast Reconciliation Toolbox"
created: 2026-05-01
updated: 2026-05-01
type: concept
tags: [forecasting, time-series, hierarchical, reconciliation, statistical, production, arxiv]
sources: [raw/papers/2604.27696.md]
---

# FoReco and FoRecoML: Forecast Reconciliation Toolbox

## Summary

Girolimetto et al. (2026) release two R packages — **FoReco** (classical linear reconciliation) and **FoRecoML** (regression + ML-based reconciliation) — that jointly cover cross-sectional, temporal, and cross-temporal reconciliation for hierarchical/grouped time series. This is the first unified toolbox bridging the classical HTS/GTS literature with modern ML-based reconciliation approaches.

## Key Findings

### What Forecast Reconciliation Is

When you have a hierarchical structure — e.g., product-level → category-level → division-level sales forecasts — bottom-up and top-down approaches are suboptimal. Reconciliation optimally combines forecasts across levels while respecting linear constraints (e.g., division sum = sum of categories). The insight: coherence doesn't cost accuracy; it often improves it.

### Three Reconciliation Dimensions

1. **Cross-sectional**: Same time, different aggregation levels (e.g., regional → national)
2. **Temporal**: Different time granularities (daily → weekly → monthly)
3. **Cross-temporal**: Both cross-sectional AND temporal simultaneously

### FoReco vs FoRecoML

- **FoReco**: Implements classical/optimal (trace) minimization approaches — MinT, structural scaling, CO(2)LS, etc. Linear, fast, well-understood.
- **FoRecoML**: Regression-based + ML approaches (XGBoost, LightGBM, neural nets) for reconciliation. Can capture nonlinear relationships between levels that linear methods miss.

### Practical Implications

- Nixtla's `hierarchicalforecast` library covers cross-sectional + temporal reconciliation in Python, but FoReco's cross-temporal coverage (simultaneous spatial + temporal aggregation) is notably broader for complex hierarchies.
- The paper demonstrates that ML-based reconciliation outperforms linear methods when relationships between series levels are nonlinear — relevant for portfolios with complex product/geography interactions.
- Default settings are sensible enough for practitioners to use without deep expertise.

## Techniques Applicable to Production Forecasting

- **Hierarchical forecasting** for portfolio-level or entity-level TS: apply reconciliation to bottom-up your granularity
- **Cross-temporal reconciliation** when you need coherent forecasts at multiple horizons (daily/weekly/monthly)
- Combining Nixtla's base forecasts with FoReco's reconciliation for production-grade hierarchical systems
- The FoRecoML ML-based approaches are worth testing when linear assumptions between hierarchy levels clearly don't hold

## My Notes

As someone building production forecasting systems: hierarchical reconciliation is underused in finance. Most teams either do naive bottom-up or top-down — both lose information. The reconciliation step is computationally cheap post-hoc and often materially improves forecast accuracy at aggregated levels (where most resource allocation decisions happen).

The cross-temporal piece is particularly interesting for rolling forecasts: if you're issuing 1-day, 1-week, and 1-month ahead forecasts, making them mutually consistent (rather than generating each independently) should reduce confusion for downstream stakeholders and may improve each individually.

The ML-based reconciliation (FoRecoML) is the novel part — linear MinT-style reconciliation has been in Nixtla's `hierarchicalforecast` for a while. The regression+gradient boosting approach lets you capture nonlinear cross-level relationships that would violate linear constraints.

## Links

- [[probabilistic-electricity-forecasting-evaluation]] — related evaluation methodology; both address practical forecast quality measurement
- [[specialist-routing-volatility]] — regime-dependent model selection; reconciliation is another form of model combination
- [Nixtla hierarchicalforecast](https://nixtlaverse.nixtla.io/hierarchicalforecast/) — Python equivalent
- [FoReco R package](https://cran.r-project.org/package=FoReco)
- [arXiv:2604.27696](https://arxiv.org/abs/2604.27696)
