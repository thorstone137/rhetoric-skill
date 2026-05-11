# v1.0.0 — Rhetoric Skill

A 10-pass editorial skill for Claude Code. Audits LLM-facing markdown (`CLAUDE.md`, `SKILL.md`, agent prompts, system prompts) using Richard Lanham's *Economics of Attention*, the Paramedic Method, and Anthropic's emotive findings. Proposes rewrites with reliability scores. You ratify; the skill applies in a separate turn.

## What it does — a worked example

A real fragment from a real `CLAUDE.md`, with Pass 0 (Paramedic) and Pass 9 (Emotive) findings:

### Before

```
It is critically important that careful attention be paid by the assistant
to the verification of all factual claims that are made in the output, as
failures in this area have been observed to result in significant degradation
of trust between the user and the system. Do not make things up.
```

### Findings

| Pass | Finding | R_eff | Source |
|------|---------|-------|--------|
| 0 | Hidden agency ("attention be paid by the assistant"); 4-link prepositional chain ("of all factual claims that are made in the output"); weak verb stack | 0.81 | Paramedic — Lanham, *Revising Prose* |
| 9 | Surveillance frame ("have been observed to result"); shame trigger ("Do not make things up") | 0.39 | Anthropic emotive findings (April 2026) |

### After (proposed — you ratify)

```
Verify factual claims before stating them. Unverified claims degrade trust.
If you don't know, say so.
```

52 words → 18 words. Active voice. Behavioral instruction replaces shame frame. The same activation now lands on every turn instead of competing with its own scaffolding.

The skill writes this proposal to `.scratchpad/`. You approve, decline, or edit. Nothing applies until you say so.

## Install

```bash
mkdir -p .claude/skills/rhetoric
curl -sL https://raw.githubusercontent.com/thorstone137/rhetoric-skill/v1.0.0/SKILL.md \
  > .claude/skills/rhetoric/SKILL.md
```

Then in Claude Code:

```
/rhetoric path/to/CLAUDE.md
/rhetoric .claude/skills/my-skill/SKILL.md --audit
/rhetoric --portfolio ".claude/skills/**/SKILL.md"
```

## Ten passes

| Pass | Audit |
|------|-------|
| 0 | Paramedic Method — sentence surgery |
| 1 | Stuff and Fluff — structure as primary |
| 2 | Attention Budget — token economics |
| 3 | Field Design — simultaneous vs linear |
| 4 | Notation Match — alphabet selection |
| 5 | AT/THROUGH Separation — toggle management |
| 6 | Scale Check — complexity audit |
| 7 | Activation Audit — virtuality check |
| 8 | Revision Readiness — structural modularity |
| 9 | Emotive Channel Audit — activation side effects |

## What's next

See [ROADMAP.md](ROADMAP.md) — Pass 0 standalone mode, emobar measurement adapter, `--diff` mode for pre-commit hooks. Tracked in issues #1-#6.

## Commercial use

The skill is MIT-licensed for personal and research use. Commercial use (inside a company, packaged as a deliverable for clients, embedded in a product) requires the paid license. Includes worked-example library, portfolio-mode walkthrough, and 12 months of updates. See [Gumroad listing — link to follow].

## Theoretical grounding

- Richard Lanham, *The Economics of Attention* (Chicago, 2006)
- Richard Lanham, *Revising Prose* (Paramedic Method)
- Anthropic, *"Emotion Concepts and their Function in a Large Language Model"* (April 2026)

Citations are inline per finding. The skill teaches the framework as it audits.
