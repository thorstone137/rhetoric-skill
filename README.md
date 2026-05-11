# Rhetorical Engineering for Claude Code

A 10-pass editorial skill that audits and rewrites LLM-facing markdown — `CLAUDE.md`, `SKILL.md`, agent definitions, system prompts — using Richard Lanham's *Economics of Attention*, the Paramedic Method, and Anthropic's emotive findings.

Most prompt files are written for human readers. The model that consumes them needs different structure: addressable regions, deterministic activation tokens, separated meta and content, decompressed prohibition stacks. This skill applies a sentence-level grammar audit (Pass 0) then nine attention-economics passes (1–9) and produces concrete rewrites with reliability bookkeeping.

## What you get

- `SKILL.md` — the full skill (10 passes, ADI inference protocol, Gamma Quintet reliability calculus, DRR ledger, portfolio mode)
- `examples/` — three before/after transformations on real prompt files
- `LICENSE.md` — commercial use license (single-developer, single-organization, OEM tiers)

## Install

```bash
# In your Claude Code project
cp SKILL.md .claude/skills/rhetoric/SKILL.md
```

Then invoke:

```
/rhetoric path/to/CLAUDE.md
/rhetoric .claude/skills/my-skill/SKILL.md --audit
/rhetoric --portfolio ".claude/skills/**/SKILL.md"
```

## What it does

| Pass | Audit | Example finding |
|------|-------|-----------------|
| 0 | Paramedic Method (sentence surgery) | Hidden agency, weak verbs, prepositional chains |
| 1 | Stuff and Fluff | Buried constraints inside narrative paragraphs |
| 2 | Attention Budget | Redundant restatements, filler phrases |
| 3 | Field Design | False sequences ("first... then... finally...") |
| 4 | Notation Match | Prose used for comparisons (should be tables) |
| 5 | AT/THROUGH Separation | Meta-instructions blended with content |
| 6 | Scale Check | Theatrical complexity (sections that don't change behavior) |
| 7 | Activation Audit | Folk psychology ("understand", "think carefully") |
| 8 | Revision Readiness | Cross-references that calcify the document |
| 9 | Emotive Channel Audit | Shame frames, surveillance lists, double binds |

Each pass runs as an Abduction–Deduction–Induction mini-cycle. Findings carry reliability scores (R_eff) computed under the Gamma Quintet. The skill proposes; the user ratifies (Transformer Mandate). All edits are reversible via git or scratchpad backup.

## Why this exists

LLM-facing documents are infrastructure. They activate the patterns that produce every downstream token. A sloppy `CLAUDE.md` doesn't fail loudly — it costs precision on every generation, compounding silently across thousands of turns. This skill makes that cost visible and gives you a deterministic path to fix it.

## Theoretical grounding

- Richard Lanham, *The Economics of Attention* (Chicago, 2006)
- Richard Lanham, *Revising Prose* (Paramedic Method)
- Anthropic, "Emotion Concepts and their Function in a Large Language Model" (April 2026)
- Structured Abductive–Deductive–Inductive inference protocol

Citations are inline. The skill teaches the framework as it audits.

## Support

Email the address in your purchase receipt. Issues, feature requests, and skill compositions welcome.
