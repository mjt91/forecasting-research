---
title: Wiki Schema
created: 2026-04-18
updated: 2026-04-18
type: meta
tags: [meta]
sources: []
---

# Wiki Schema

## Domain
Time series forecasting research — focused on methods, models, and applications in finance. Spans academic papers, blog posts, and practitioner notes on improving forecasting systems in production.

## Conventions
- File names: lowercase, hyphens, no spaces (e.g., `nhits-2023.md`)
- Every wiki page starts with YAML frontmatter (title, created, updated, type, tags, sources)
- Use `[[wikilinks]]` to link between pages (minimum 2 outbound links per page)
- When updating a page, always bump the `updated` date
- Every new page must be added to `index.md` under the correct section
- Every action must be appended to `log.md`

## Frontmatter
```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: paper | article | concept | model | dataset | method
tags: [from taxonomy below]
sources: [URL or raw/...]
---
```

## Tag Taxonomy
Add new tags here BEFORE using them:
- `forecasting` — general forecasting topics
- `time-series` — time series specific
- `transformer` — transformer-based methods
- `neural-net` — neural network architectures
- `statistical` — classical statistical methods
- `finance` — financial applications
- `production` — MLOps, deployment, monitoring
- `arxiv` — sourced from arXiv
- `blog` — blog posts, articles
- `data` — datasets

## Page Thresholds
- **Create a page** when a paper/concept is central to one source or appears in 2+ sources
- **Add to existing page** when new information extends what's already covered
- **DON'T create a page** for passing mentions or minor details
- **Split a page** when it exceeds ~200 lines

## Update Policy
Newer sources generally supersede older ones. If contradictory, note both with dates and flag.
