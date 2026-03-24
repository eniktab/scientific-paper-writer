# claude-scientific-paper-writer

A Claude Code skill for writing publication-ready scientific manuscripts targeting top-tier journals. The only skill in this space that **fetches live journal requirements** — author guidelines, AI disclosure policy, word limits, and LaTeX template — before writing a single sentence.

Works with Claude Code, Codex CLI, Gemini CLI, Cursor, and any agent that follows the [Agent Skills](https://agentskills.io) open standard.

---

## What makes this different

| Feature | This skill | Other scientific writing skills |
|---------|-----------|----------------------------------|
| Journal requirements | Fetched live via WebSearch/WebFetch | Hardcoded (go stale) |
| AI authorship policy | Fetched per journal | Not addressed |
| LaTeX template | Downloaded from journal/Overleaf | Generic template |
| AI-voice removal | 25 patterns, systematic audit | Not addressed |
| Citation verification | WebSearch confirms every DOI | No verification |
| Sentence rhythm guidance | Perplexity + burstiness mechanics | Not addressed |
| Reporting guidelines | CONSORT, PRISMA, STROBE, ARRIVE, TRIPOD-ML, CARE, STARD, SQUIRE, COREQ | Named only |
| Statistical reporting | Complete format per test type (effect size, CI, exact P) | Partial |
| Coverage | Any journal, any field | Nature-family only |

---

## Install

```bash
# Single file — copy to your user-level skills directory
cp skills/scientific-paper-writer/SKILL.md ~/.claude/skills/scientific-paper-writer.md
```

Or for a specific project only:

```bash
mkdir -p .claude/skills/scientific-paper-writer
cp skills/scientific-paper-writer/SKILL.md .claude/skills/scientific-paper-writer/SKILL.md
```

---

## Use

Invoke with `/scientific-paper-writer` in Claude Code, then describe your task:

```
/scientific-paper-writer Write an Article for Nature Biotechnology on our new
base-editing method. Data: efficiency.csv (5 cell lines, n=200 each).
Key finding: 94% efficiency in HEK293, 3.2-fold over Cas9 (P < 0.001).
```

The skill will:
1. Fetch Nature Biotechnology's current submission guidelines
2. Extract word limits, figure limits, abstract format, citation style
3. Fetch their AI authorship policy and required disclosure language
4. Find and link the current LaTeX template
5. Check recent editorial priorities and desk-rejection criteria
6. Write the paper to those exact requirements with verified citations

---

## Core capabilities

### Live journal intelligence (Phase 1a)
Before writing anything, the skill fetches the target journal's author guidelines page, extracts all format requirements into a `journal_profile.yaml`, fetches the AI authorship policy separately, and downloads the current LaTeX template. The profile becomes the single source of truth for all formatting decisions — overriding any defaults in the skill.

Covers any journal: Nature family, Cell Press, Elsevier, Wiley, Springer, PLOS, PNAS, ACS, RSC, IEEE, ACM, and conference proceedings.

### Authentic scientific voice — 25 AI-pattern audit
Every draft is audited against 25 AI writing patterns (based on [Wikipedia: Signs of AI Writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) and the [blader/humanizer](https://github.com/blader/humanizer) framework) before delivery:

- **Content**: significance inflation, vague attributions, superficial -ing analyses, formulaic narratives
- **Language**: AI vocabulary (`pivotal`, `landscape`, `delve`, `crucial`, `leverage`, etc.), synonym cycling, copula avoidance, negative parallelisms
- **Style**: em-dash overuse, inline-header lists, uniform sentence length
- **Filler**: stacked hedges, generic conclusions, filler phrases (`in order to` → `to`)

Includes guidance on **perplexity** (word-choice surprise) and **burstiness** (sentence-length variation) — the two metrics AI detectors actually measure.

### Citation verification
Every reference is confirmed via WebSearch before inclusion. Unverifiable sources are flagged `[UNVERIFIED — confirm before submission]` and excluded from the bibliography. Zero hallucinated references.

### Statistical reporting
Complete format for every test type: t-test, ANOVA, correlation, regression, survival analysis, meta-analysis, Bayesian statistics. Reports test statistic + df + exact P-value + effect size + 95% CI as a minimum for every comparison.

### Reporting guidelines
Systematic verification against the appropriate checklist — not just naming it:
CONSORT 2010, PRISMA 2020, STROBE, ARRIVE 2.0, STARD 2015, TRIPOD, TRIPOD-ML, CARE, SQUIRE 2.0, COREQ, SRQR.

### Nature storytelling framework
Four-move funnel introduction, "Here we show" construction, central-claim test, results-as-logical-progression structure — all derived from Nature's own editorial guidance.

### Full lifecycle
- Grant proposals (NIH R01, ARC Discovery, NSF)
- Peer review response letters
- Cover letters
- Pre-submission quality checklist (35 items)
- Field-specific conventions: molecular biology, ML/AI, clinical, ecology, physics, psychology

---

## What the output looks like

After running, the project directory contains:

```
writing_outputs/YYYYMMDD_topic/
├── journal/
│   ├── journal_profile.yaml          ← live-fetched format requirements
│   ├── journal_profile_summary.md    ← human-readable summary
│   ├── ai_policy.md                  ← exact disclosure language required
│   └── latex_template/               ← downloaded journal template
├── manuscript/
│   ├── main.tex                      ← uses journal's template class
│   └── main.bib                      ← verified BibTeX
├── sources/
│   ├── references.bib                ← all verified references
│   └── search_log.md                 ← what was searched, what was found
└── cover_letter.md
```

---

## Examples

```
# Any journal — auto-detected format
/scientific-paper-writer Write a Research Article for PLOS Computational Biology
on our DNA tokenization benchmarks. I'll provide benchmark_results.csv.

# Anti-AI voice audit only
/scientific-paper-writer Run the AI-voice audit on this draft: [paste text].
List every pattern found and rewrite each flagged sentence.

# Peer review response
/scientific-paper-writer Write a complete response letter to these reviewer comments
for my Genome Biology submission: [paste comments]

# Grant proposal
/scientific-paper-writer Write the Specific Aims page and Significance section
of an NIH R01 on NAD+ metabolism in aging. FOA: PA-23-065.

# Journal requirements lookup only
/scientific-paper-writer Look up current submission requirements for
Nucleic Acids Research, Database Issue. I need word limits, AI policy,
and the LaTeX template.
```

---

## Compatibility

Follows the [agentskills.io](https://agentskills.io/specification) open standard.

| Platform | Compatible |
|---------|-----------|
| Claude Code | Yes |
| Codex CLI | Yes |
| Gemini CLI | Yes |
| Cursor | Yes |
| VS Code + Copilot | Yes |
| OpenHands | Yes |
| Roo Code | Yes |

---

## License

MIT — see [LICENSE](LICENSE)

---

## Contributing

Issues and PRs welcome. If a journal's guidelines page structure breaks the lookup (layouts change), open an issue with the journal name and we'll update the URL patterns.
