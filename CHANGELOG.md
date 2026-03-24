# Changelog

## [1.0.0] — 2026-03-24

### Added
- Phase 1a: Live journal intelligence gathering — fetches author guidelines, AI policy, and LaTeX template for any journal via WebSearch/WebFetch before writing
- `journal_profile.yaml` schema with 20+ fields extracted from live guidelines
- AI authorship policy lookup — exact disclosure language per journal
- LaTeX template discovery (Overleaf gallery, publisher template hubs)
- Editorial priority and desk-rejection criteria lookup
- 25 AI writing pattern audit (Content / Language / Style / Communication / Filler categories)
- Perplexity and burstiness mechanics for authentic voice
- "The Soul Factor" guidance on intellectual commitment and analytical specificity
- Nature storytelling framework: four-move funnel, "Here we show", central-claim test
- Statistical reporting standards for all test types with effect sizes and confidence intervals
- Reporting guideline verification: CONSORT, PRISMA, STROBE, ARRIVE 2.0, STARD, TRIPOD, TRIPOD-ML, CARE, SQUIRE, COREQ, SRQR
- Open science section: FAIR data checklist, preregistration guidance, data/code availability statements
- Grant proposal guides: NIH R01, ARC Discovery, NSF
- Peer review response letter template with rules
- Cover letter template
- Field-specific conventions: molecular biology/genomics, ML/AI, clinical/biomedical, ecology, physics/engineering, psychology/social sciences
- 35-item pre-submission quality checklist
- Structured output directory with `journal/` subdirectory for fetched profile and template
