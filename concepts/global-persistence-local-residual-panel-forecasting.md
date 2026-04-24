---
title: "Global Persistence, Local Residual Structure for Panel Forecasting"
created: 2026-04-24
updated: 2026-04-24
type: concept
tags: [forecasting, time-series, finance, panel-forecasting, hierarchical, heterogeneous-effects]
sources: [raw/papers/2604.09821.md]
---

# Global Persistence, Local Residual Structure for Panel Forecasting

## Summary

Roshka (2026) shows that on heterogeneous investment panels mixing macro and firm-level data, a two-stage architecture (global pooled AR for shared persistence + block-specific local models for residuals) significantly outperforms both pure global and pure local approaches. The key insight: data-type heterogeneity — not just cross-sectional heterogeneity — is what drives the gain. The block decomposition matters when the panel mixes fundamentally different data types (macro vs. firm-level), not just different sectors.

## Key Findings

- **Two-stage architecture beats both pure global and pure local**: Global AR captures shared persistence across all actors; block-specific local models capture residual dynamics that differ by data-type block.
- **Data-type heterogeneity is the operative condition**: The gain disappears on homogeneous panels (firm-only). Mixed-type panels (macro + firm) are where block decomposition helps — because macro factors misrepresent some firms' dynamics.
- **Architectural, not methodological gain**: Per-actor gradient boosting with the same block structure doesn't fully close the gap. The advantage comes from combining block-specific estimation with low-rank factor extraction, not from any particular estimator.
- **Tech/health block drives 72% of the gain**: Suggests that for sectors with strong macro sensitivity (tech, health), the global factor augmentation actively hurts — local treatment is essential.
- **Held-out decade validation**: 2005-2014 frozen, evaluated on 2015-2024 — strong out-of-sample evidence.

## Techniques Applicable to Production Forecasting

- **Hierarchical/top-down reconciliation**: The two-stage approach is a form of hierarchical reconciliation — global level captures cross-unit persistence, local levels capture unit-specific residual structure. Directly relevant to Nixtla's hierarchical forecasting capabilities.
- **Block decomposition**: Partition your panel by data type before modeling — not just by unit. If you have macro features + unit-level features, treat them differently.
- **Mixed-type panel modeling**: When your panel mixes fundamentally different data generating processes (macro vs. micro, different sectors), a single global model is likely suboptimal. Block-specific residual models can help.
- **Robustness to macro factor misspecification**: Since macro factors can actively degrade forecasts for some units, consider dropping macro augmentation for units where it hurts.

## My Notes

As a production forecasting practitioner: this paper connects to hierarchical reconciliation in the Nixtla stack (`hierarchicalforecast` library). The Nixtla approach handles cross-sectional hierarchies well, but this paper's contribution is specifically about mixing different data types (macro + micro) in a panel — which creates a different kind of heterogeneity than standard hierarchical.

The practical lesson: if you're forecasting a panel that includes both macro-driven and firm-level dynamics (common in credit, equities, or macro finance), consider a two-stage approach where macro factors are only applied where they're relevant, and unit-specific residuals are modeled separately.

The 72% concentration in tech/health is a useful heuristic: high-duration, high-sensitivity sectors are where macro augmentation hurts most. For more commoditized, domestically-focused businesses, global macro factors may still be helpful.

## Links

- [[hierarchical-forecasting]] — Nixtla's hierarchical forecasting approach
- [[panel-data-forecasting]] — broader panel TS literature
- [arXiv:2604.09821](https://arxiv.org/abs/2604.09821)
- [Nixtla hierarchicalforecast](https://nixtlaverse.nixtla.io/hierarchicalforecast/) — production hierarchical reconciliation
