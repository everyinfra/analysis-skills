# Changelog

Future content or contract changes must bump the package version and add a dated entry.

## 0.4.1 - 2026-10-15

- **License correction for `spreadsheet-deliverable`**: 0.4.0 credited the xlsx skill in anthropics/skills as MIT. That skill is source-available under Anthropic's own terms, which do not permit derivative works, so the credit was wrong. `spreadsheet-deliverable` has been rewritten from public guidance (ICAEW Financial Modelling Code, openpyxl documentation, Microsoft [MS-XLSX]); the anthropics/skills reference is removed from the skill, `analysis-foundation` and NOTICE.
- NOTICE: each credited repository now lists the license it declares (checked 2026-10-15) instead of "(open)".
- README version line corrected (it still said 0.3.0).

## 0.4.0 - 2026-10-09

- **New skill `spreadsheet-deliverable`**: xlsx delivery discipline — formula-first cells (never hardcode results), recalculation gate with zero-error report before delivery, dual-pass reading model, LibreOffice compatibility list, input/formula/cross-sheet/fill color conventions, percentages stored as decimals, assumptions with source annotations; analysis-scenario patterns (weighted scorecard with sensitivity, comparison matrix with thresholds, trend+anomaly sheets).
- **Gold-standard sample output** (`examples/gold-standard-review-insights.md`, synthetic data): demonstrates the seven-section deliverable standard — answer-style title, standalone "The answer", numbers with denominators, option table, "What could change this conclusion", method notes.

## 0.3.0 - 2026-10-09

Adds a shared discipline layer and domain references, mined from high-star open-source analysis skills (each source linked in-file):

- **New skill `analysis-foundation`**: the shared analysis discipline for all skills — mandatory four-step pipeline (profile→filter→aggregate→verify; no one-shot answers), numeric-integrity rules (every number computed by code; LLM RAG numeric recall can be as low as 25.7%, DABstep top agents ~16%), denominator-naming, n<30 no rates, uncertainty reporting, correlation-vs-causation wording, survivorship and MNAR checks, metric-formula locking, chart-choice table, method-notes template (REFORMS-aligned), LLM labeling calibration protocol, empty-result root-cause checklist.
- `social-content-performance` + `references/metrics-and-benchmarks.md`: dual engagement-rate denominators (up to 10x apart), sourced 2025–26 benchmark table (Rival IQ 4M posts / Socialinsider), signal-vs-vanity metrics, A/B discipline, exposure confounding.
- `review-insights` + `references/aspect-mining.md`: ABSA four-tuple schema with mandatory quotes, BERTopic-vs-LDA-vs-LLM tradeoffs, hybrid pipeline, rating-sentiment divergence, MNAR statements.
- `ecommerce-product-analysis` + `references/weighted-scoring-and-pricing.md`: MCDA weighted scoring with sensitivity, three-tier price-band template, Keepa-model price-history metrics, Google Product Taxonomy variant grouping.
- `content-analysis-tagging` + `references/taxonomy-quality.md`: MECE design limits, four quality metrics incl. two-pass kappa, gold-set calibration (>80% agreement gate, 5–10% human audit).

## 0.2.0 - 2026-09-26

Adds `review-insights`: pain points, praise, and rating patterns from review records, with a synthetic `amazon/reviews` example in `examples/`.

## 0.1.0 - 2026-09-26

Initial public package. Ships three analysis Skills, each with a synthetic example (`source_response`, `task`, `expected_output`) in `examples/`:

- `ecommerce-product-analysis`
- `social-content-performance`
- `content-analysis-tagging`
