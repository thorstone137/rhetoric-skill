# Roadmap

Public list of what's planned. Estimated dates; PRs and issues against any item are welcome.

## v1.1 — within 14 days

| Item | Why | Issue |
|------|-----|-------|
| Standalone Pass 0 audit-only mode | Many users want the Paramedic regex bank without the full ADI cycle for pre-commit hooks | #1 |
| DRR ledger integration with `bd remember` | Cross-session recurrence detection without re-reading scratchpad | #2 |
| emobar v3.1 measurement adapter | Lifts Pass 9 R_eff from 0.39 (trace floor) to 0.95 (measured) | #3 |

## v1.2 — within 30 days

| Item | Why | Issue |
|------|-----|-------|
| `--diff <commit>` mode | Audit only the lines a commit changed; pre-commit hook usable | #4 |
| `<rhetoric-suppress>` inline tags | False-positive control without code-block hacks | #5 |
| Per-pass JSON output | Downstream tooling integration (CI, dashboards) | #6 |

## v2.0 — exploratory

- Multi-language support (Pass 0 regex bank for prompts written in non-English)
- LLM-as-judge corroboration: a second model rates the proposed rewrite against the original on attention-allocation criteria, raising R_eff above 0.39 without requiring user ratification for low-stakes findings
- Skill composition: `/rhetoric` chained with `/dhh-rails-reviewer`-style domain-specific rewriters

## Not planned

- Auto-apply mode without user ratification — Transformer Mandate is structural, not optional
- Web UI — the skill operates inside Claude Code; a web wrapper would dilute, not add
- Embedding-based "similar prompt" suggestions — adds stochasticity to a deterministic protocol

## Discussion

Open an issue to propose. Roadmap items move based on what the user community actually exercises, not announced intent.
