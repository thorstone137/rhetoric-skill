# Changelog

All notable changes to the Rhetoric Skill. Format: [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Versioning: [SemVer](https://semver.org/).

## [Unreleased]

Planned for v1.1 (target: rolling within 14 days):
- Pass 0 regex bank exposed as a standalone audit-only mode (`--pass 0 --audit-only`)
- DRR ledger `bd remember` integration for cross-session recurrence detection
- emobar v3.1 measurement adapter — Pass 9 lifts from F1 (cited principle) to F2 (measured channel delta)

Planned for v1.2:
- `--diff <commit>` mode: audit only the lines changed in a commit, scoped for pre-commit hook usage
- Inline `<rhetoric-suppress>` tags for false-positive control
- Per-pass JSON output for downstream tooling

## [1.0.0] — 2026-05-10

First public release.

### Added
- 10 editorial passes (Pass 0 Paramedic Method + Passes 1-8 *Economics of Attention* + Pass 9 Emotive Channel Audit)
- ADI inference protocol (Abduction → Deduction → Induction) per pass
- Gamma Quintet reliability calculus (IDEM, COMM, LOC, WLNK, MONO) with min-aggregation as the Gödel t-norm
- Reliability scoring (`R_eff`) per finding, externalized via deterministic regex / cited principle / measurement
- Transformer Mandate: skill proposes at L1, user ratifies to L2 in a separate turn
- DRR (Design Rationale Record) ledger for maturity-aware re-audits
- Portfolio mode (`--portfolio <glob>`) for cross-file voice coherence diagnostics
- Maturity-aware execution: skips passes that have produced zero findings across two prior runs (regression check every 5th audit)
- Auto-ignore scopes for false-positive suppression (code blocks, quotations, tables, frontmatter)

### Theoretical grounding
- Richard Lanham, *The Economics of Attention* (Chicago, 2006) — cited per pass
- Richard Lanham, *Revising Prose* — Paramedic Method
- Anthropic, "Emotion Concepts and their Function in a Large Language Model" (April 2026) — Pass 9
