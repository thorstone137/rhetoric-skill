---
name: rhetoric
description: Apply Lanham's attention economics, the Paramedic Method, and the emotive research findings as an ADI (Abduction-Deduction-Induction) protocol over LLM-facing markdown files (CLAUDE.md, SKILL.md, agent definitions, system prompts). Each of the ten editorial passes runs as an ADI mini-cycle — abduce candidates, deduce against the cited principle, induce via concrete rewrite. Reliability propagates under the Gamma Quintet (WLNK central). User approval ratifies L1→L2 (Transformer Mandate). Maintains a Design Rationale Record ledger per file for maturity-aware re-audits. Supports --portfolio <glob> for cross-file voice coherence checks.
allowed-tools: ["Read", "Write", "Glob", "Grep", "Bash"]
---
<!-- SIGIL: Hybrid (Arbiter+Scribe) / Act -->

# Rhetorical Engineering Editor

**Read-only during execution. Draft, don't apply.** Proposals go to `.scratchpad/` and the conversation. Apply runs in the follow-up turn — after the user's word, not before. Approval is the **Transformer Mandate** ratification: the skill produces L0 and L1 claims; the user ratifies them to L2.

Apply Lanham's *The Economics of Attention*, the Paramedic Method, and Anthropic's emotive findings as an ADI protocol over LLM-facing documents. Pass 0 performs deterministic sentence-level cleanup (Paramedic Method — Official Style detection). Passes 1-8 diagnose attention-allocation failures (one per *Economics of Attention* chapter). Pass 9 audits emotional activation side effects. Each pass runs as an Abduction-Deduction-Induction mini-cycle; reliability propagates under the Gamma Quintet, with WLNK ensuring no proposal exceeds the reliability of its weakest premise.

**Theory:** `docs/Feature-Design/Active-Research/Richard-Lanham/rhetorical-engineering-chapter-instructions.md`
**Inference protocol:** `docs/Feature-Design/Active-Research/STRUCTURED-ABDUCTIVE-DEDUCTIVE-INDUCTIVE.md` — ADI protocol, Gamma Quintet, WLNK, formality/layer ceilings, Transformer Mandate, DRRs
**Paramedic reference:** `docs/Feature-Design/Active-Research/Richard-Lanham/lanham-paramedic-method.pdf` — Lanham's sentence-level revision protocol targeting Official Style (noun stacks, passive voice, hidden agency, prepositional chains)
**Handlist reference:** `docs/Feature-Design/Active-Research/Lanham-Handlist-of-Rhetorical-Terms.md` — Lanham's catalog of rhetorical figures. Consult when proposing rewrites: figures from **Brevity**, **Balance/Antithesis**, **Repetition: Words** activate do-or-die register; figures from **Amplification**, **Description**, **Example/allusion** activate fertile register.
**Prior art:** `docs/Feature-Design/Active-Research/Richard-Lanham/design-analysis/SYNTHESIS-1.1.md`
**Emotive reference:** Anthropic, *"Emotion Concepts and their Function in a Large Language Model"* (April 2026) — emotion representations are robust and causally influence behavior. Measurement model: emobar v3.1 (`/mnt/agentic-data/ai-workstation/Software-Downloads/emobar-master/README.md`)

**Scope:** Any markdown file whose audience is an LLM — CLAUDE.md, SKILL.md, agent definitions, system prompts, context-construction documents, configuration files with prose instructions.

## Arguments

`$ARGUMENTS` — one or more file paths to edit. Glob patterns accepted.

If no arguments: ask "Which LLM-facing file should I edit?"

**Flags:**
- `--audit` — Report only, don't edit (writes report to scratchpad)
- `--pass N` — Run only pass N (0-9)
- `--verbose` — Include before/after diffs in report
- `--portfolio <glob>` — Cross-file voice coherence audit (no per-file rewrites; emits divergence report). Example: `--portfolio ".claude/skills/**/SKILL.md"`
- `--force-all-passes` — Ignore maturity-aware routing; run every pass regardless of ledger state
- `--epistemic-trace` — Emit per-finding ADI trace (inference mode at each step, evidence chain, R_eff computation) into proposals.md

## Artifacts

Every run creates a timestamped folder:
```
.scratchpad/rhetoric/{YYYY-MM-DD-HHmm}/
├── proposals.md              # Proposed changes with reasoning + R_eff (always written)
├── report.md                 # Final report: what was applied, declined, why
├── {filename}.original       # Backup of original file (before any edits)
├── drrs.jsonl                # Design Rationale Records, one per finding (this run)
└── portfolio-report.md       # Portfolio mode only — cross-file coherence diagnostic
```

Persistent DRR ledger (shared across runs):
```
.scratchpad/rhetoric/_ledger/
└── {filename-slug}.json      # DRR audit history per file — drives maturity-aware execution
```

**On start:** Create the run folder. Ensure the ledger folder exists. Back up the original file before any edits. Read the ledger for the target file (if present) to inform pass selection.

---

## The ADI Inference Protocol

Each editorial pass conflates three distinct epistemic operations unless structurally separated. The protocol decomposes every pass into three explicit phases, each producing claims at a successively higher epistemic layer.

### Three modes, three layers

Abduction is constructive reasoning — the move that opens candidate space. Pick up a bow without ever firing one and you still see the curve, the string's tension, the arrow's straight shaft, the point's direction. From the parts you infer function; from function you see purpose. That sequence — parts → function → purpose — is abduction. Structural inference from familiar pattern competence. Not guesswork.

The skill's abductive phase moves the same way over a document. Read the parts (sentences, structure, token rhythm). Infer function (what each part does in the attention budget). See purpose (the document's intended activation, and where it diverges from intent). Deduction then checks each candidate against the cited principle; induction validates the rewrite against the document.

| Mode | Phase | Layer | What happens here |
|------|-------|-------|------------------|
| **Abduction** | Diagnose | L0 — Generated | Read the parts, infer function, see purpose. Multiple candidates open the search space; premature commitment costs more than the candidates that don't survive. |
| **Deduction** | Verify | L0→L1 — Substantiated | Check each candidate against the pass's cited principle. Logical consistency promotes the candidate from generated to standing. |
| **Induction** | Validate | L1→L2 — Corroborated | Propose the concrete rewrite. Empirical confirmation completes the cycle; user approval is the ratifier (see Transformer Mandate). |

**Layer ceilings (≤0.35 / ≤0.75 / ≤1.00) bound logical force, not generative quality.** A high-quality abductive reading sits at L0 with ≤0.35 reliability — not because the reading is poor, but because at L0 we don't yet have a verification pathway that lets us act on the reading as if it were established. The same reading at L1 (after deductive check against the cited principle) reaches ≤0.75; at L2 (after empirical corroboration via measurement or user ratification) it reaches ≤1.00. The progression is *force compounding through the protocol*, not *quality redeeming through verification*.

### Formality of evidence

| Pass | Evidence type | Formality | Ceiling |
|------|---------------|-----------|---------|
| 0 | Deterministic regex match against Paramedic rule | F2 (empirical) on the match, F1 (cited rule) on the principle — WLNK gives F1 | 0.85 |
| 1-8 | Cited Lanham chapter + LLM judgment about applicability | F1 | 0.85 |
| 9 (no emobar) | Cited emotive principle + LLM judgment | F1 | 0.85 |
| 9 (with emobar measurement) | emobar v3.1 channel profile delta | F2 (empirical) | 0.95 |

### Externalization unbinds reliability

Chain-of-thought traces are 25–39% faithful to the model's actual computation (Anthropic 2025). That isn't a verdict on the thinking — it's a measurement of how much the stated trace tracks the underlying process. While a finding rests on stated trace alone, its R_eff caps at 0.39. The lift comes from externalization: a deterministic match, a measurement, a citation, an external reviewer. Each externalization channels the abductive reading through an independently checkable pathway, where its force compounds past the trace floor.

| Finding type | Pathway | R_eff ceiling |
|--------------|---------|---------------|
| Pass 0 regex match | Deterministic — match speaks for itself | 0.85 |
| Pass 1-8 reading on stated trace alone | Trace-bound — awaiting externalization | 0.39 |
| Pass 1-8 reading + overlapping Pass 0 match | Externalized — the regex carries the reading | 0.85 |
| Pass 9 reading + emobar measurement | Externalized — measurement carries the reading | 0.95 |
| Pass 9 reading on stated trace alone | Trace-bound — awaiting measurement | 0.39 |

Externalization is the lever. Channel the reading through a Pass 0 match, an emobar measurement, a cited principle, or a user reviewer — the insight stays the same; the pathway is what compounds.

### Gamma Quintet (reliability invariants)

| Invariant | Statement | Application here |
|-----------|-----------|------------------|
| **IDEM** | Γ([x]) = x | A single premise retains its reliability. |
| **COMM** | Γ([a, b]) = Γ([b, a]) | Premise order does not change R_eff. |
| **LOC** | Updating premise E affects only conclusions whose chain includes E | Findings in Pass 3 do not change Pass 5's R_eff unless cross-referenced. |
| **WLNK** | Γ(S) ≤ min(S) | **Central constraint.** No proposal exceeds the reliability of its weakest premise. |
| **MONO** | a ≤ a' implies Γ([a, b]) ≤ Γ([a', b]) | Strengthening evidence cannot weaken the proposal. |

The Gödel t-norm Γ(S) = min(S) satisfies all five (Theorem 1, paper Section 4.1) and is the unique idempotent continuous t-norm (Theorem 2). This skill uses min as the within-role aggregator.

### Verification credibility multipliers

Evidence scores are scaled by source:

| Source | Multiplier |
|--------|-----------|
| Self-reported ("I think this is Official Style") | 0.60 |
| Script-attached (Pass 0 regex match, token count) | 0.85 |
| Externally reviewed (user approval, peer comment) | 0.95 |
| Executed-and-verified (emobar measurement, deterministic re-check on rewrite) | 1.00 |

### WLNK worked example (rhetoric application)

A Pass 1 proposal: "Convert this paragraph to a table."

| Premise | Source | State | R |
|---------|--------|-------|---|
| p1 — "this paragraph compares X and Y" | Abductive reading of the prose | Generated, awaiting externalization | 0.39 × 0.60 = 0.23 |
| p2 — Lanham Ch 1: structure-as-primary | Cited principle (the framework's canon) | Standing | 0.85 × 0.95 = 0.81 |
| p3 — Tables activate contrastive patterns | Lanham notation guide (Pass 4 table) | Standing | 0.85 × 0.95 = 0.81 |

R_proposal = min(0.23, 0.81, 0.81) = **0.23** — bounded by the un-externalized reading. The reading itself may be entirely correct; what the bound tracks is *what the reading alone can establish*.

Channel p1 through a deterministic pathway: run a Pass 0 regex over the passage. If comparative markers concentrate where the prose compares X and Y, the regex carries the reading. p1 moves to F2 script-attached (0.95 × 0.85 = 0.81), and R_proposal rises to min(0.81, 0.81, 0.81) = **0.81**.

The same insight, two pathways. The bookkeeping rewards externalization not because the reading was weak, but because protocol force compounds through verifiable channels. A proposal at R_eff = 0.23 stays L0; the same proposal at R_eff = 0.81 reaches L1 and becomes a candidate for user ratification to L2.

### Transformer Mandate

The skill makes the case at L1; the user lives with the document long enough to know whether the change holds. The L1→L2 ratification — the move from "logically consistent with the cited principle" to "empirically corroborated as an improvement to this document" — sits with the entity that has the longer time horizon. That entity is the user.

| Step | Who acts | Layer transition |
|------|----------|------------------|
| Generate candidates | Skill (Abduction) | — → L0 |
| Check candidates against principle | Skill (Deduction) | L0 → L1 |
| Approve and apply rewrite | User (Induction completes) | L1 → L2 |

The boundary is structural, not punitive. The skill produces strong L1 claims; the user's word is what closes the cycle.

### Two-tier aggregation

Within a pass (Tier 1): aggregate findings by epistemic role.

| Role | Operator | Use case |
|------|----------|----------|
| Structural gates | min (Gödel t-norm) | Pass 0 deterministic violations, factual contradictions |
| Quality reviews | min (Gödel t-norm) | Lanham judgment calls — kept conservative under trace floor |
| Performance metrics | conservative OWA over emobar deltas | Pass 9 channel-profile measurements |

Across passes (Tier 2): min — preserves WLNK across the proposal aggregate. If any pass surfaces a finding at R_eff = 0.23, the document's overall R_eff is capped at 0.23.

---

## The Ten Passes (0-9)

Run Pass 0 first (deterministic Paramedic cleanup). Then run passes 1-8 sequentially. Each pass reads the current state of the file (including changes from prior passes). Each pass produces specific edits, with rationale captured in `proposals.md` and per-finding DRRs in `drrs.jsonl`. Pass 9 (Emotive Channel Audit) runs last as a cross-cutting review.

**Pass ordering rationale:**
- **Pass 0** runs first because sentence-level bloat obscures the signal that passes 1-9 operate on. A table built from Official Style is Official Style wearing a table. Paramedic surgery on the sentence before architectural passes on the document. Pass 0's deterministic findings also raise R_eff for Passes 1-8 by externalizing LLM judgments.
- **Passes 1-8** apply Lanham's attention-economics framework (one per chapter of *The Economics of Attention*).
- **Pass 9** runs last as a cross-cutting review of emotional side effects from the framing that passes 1-8 leave in place.

**Maturity-aware execution (rhetorical debt ledger):**

If `.scratchpad/rhetoric/_ledger/{filename-slug}.json` exists AND the file's SHA-256 hash matches the hash recorded at the last audit (no intervening user edits), route passes as follows:

| Ledger state for pass N | Action this run |
|------------------------|----------------|
| No prior entry (cold) | Run pass N |
| Last 2 runs produced zero findings | Skip pass N (note in report); run every 5th audit for regression check |
| Same finding fingerprint recurred ≥2 runs | Run pass N; escalate finding as rhetorical debt; raise its credibility by recurrence weight |
| Findings applied last run, no recurrence yet | Run pass N normally |

If the file's hash differs from the ledger (user edited externally), run all passes regardless. `--force-all-passes` overrides all routing.

---

### Pass 0: Paramedic Method (Sentence-Level Surgery)

**Lanham grounding:** *Revising Prose* (Paramedic Method) — see `lanham-paramedic-method.pdf`.

**Question:** Does each sentence have a visible actor and active verb, or has Official Style obscured agency in noun stacks and passive voice?

**Target disease — Official Style:**
- Built on nouns, often abstractions, often Latinate ending in *-tion*
- Noun-clusters (adjective replaced by noun)
- Passive/impersonal action — no visible actor
- No active verbs, no direct objects ("Who's kicking who?" returns nothing)
- Euphemism replacing plain verbs (*"Learning Facilitator"* for *teacher*, *"utilize"* for *use*)
- Motion converted to stasis, concealing agency

**Abduction (L0 — Generated): Generate candidate sentences.** Apply the deterministic detection rules below. Each match is an L0 candidate carrying a regex fingerprint.

| Symptom | Detection rule |
|---------|----------------|
| Prepositional chains | >2 prepositions (*of, in, for, at, by, with, from, to*) per sentence |
| Weak verbs | Copular/passive constructions (*is, are, was, were, has, have, be, been, will be, would be*) without an adjacent strong verb |
| Hidden agency | Passive voice (subject receives action) with no named agent |
| -tion stacks | ≥2 abstract *-tion/-sion/-ment/-ance* nouns in a single sentence |
| Slow starts | Sentences beginning with *"It is"*, *"There is"*, *"The purpose of"*, *"It should be noted"*, *"One of the"*, *"In order to"* |
| Latinate substitution | *utilize* (use), *commence* (start), *terminate* (end), *facilitate* (help), *implement* (do) |

**Auto-ignore scopes (false-positive guards):**
- Code blocks (fenced by triple backticks or indented 4+ spaces)
- Inline code (between backticks)
- Direct quotations (cited material may legitimately use Official Style)
- Table cells (terse is expected)
- YAML frontmatter
- URLs and file paths

**Deduction (L0→L1 — Substantiation):** The regex match IS the deductive verification. The match is F2 (empirical, deterministic) carrying script-attached credibility 0.85 → R(match) = 0.95 × 0.85 = 0.81. The rule is F1 (cited Paramedic principle) carrying externally-reviewed credibility 0.95 → R(rule) = 0.85 × 0.95 = 0.81. WLNK: **R_eff = min(0.81, 0.81) = 0.81**. Promote to L1.

**Induction (L1→L2 — Corroboration via Transformer Mandate): Propose concrete rewrite.** Apply Lanham's 9-step protocol:

1. Circle prepositions; collapse chains (target 0-2 per sentence)
2. Circle weak verbs; replace with active verbs
3. Ask "Who's kicking who?"; expose the agent
4. Lead with the actor
5. Put the action in a simple active verb (one word when possible)
6. During revision, put each sentence on its own line
7. Delete slow starts
8. Vary sentence length (monotone rhythm signals Official Style)
9. Read aloud — does it sound like an instruction or a committee memo?

Verify the rewrite with a deterministic re-check: run the same regex over the proposed rewrite. If any Pass 0 symptom remains, the rewrite has not corroborated — return to step 1. User approval ratifies L1→L2.

**Example transformation:**
```
BEFORE (5 prepositions, 2 weak verbs, -tion stack, hidden agency):
  The initialization of the dispatch mechanism will be performed
  after verification of the prerequisites is complete.

AFTER (0 prepositions, 2 active verbs, visible agent):
  Verify prerequisites, then dispatch.
```

**Example transformation:**
```
BEFORE (slow start + -tion stack):
  It is widely known that the implementation of validation
  of the inputs should occur prior to execution.

AFTER (actor-led, active):
  Validate inputs before execution.
```

**Pass 0 fingerprint format** (for ledger):
`{symptom}@{line-range}:{snippet-slug}` — e.g., `weak-verb-stack@L23-L24:initialization-of-verification`

**Reliability:** F1 (rule) ∧ F2 (match). WLNK → R_eff ≤ 0.81 (script-attached). The trace floor does not apply — the regex carries the reading.

---

### Pass 1: Stuff and Fluff (Structure as Primary)

**Lanham grounding:** Ch 1 — Stuff and Fluff. Structure as primary attention-allocation mechanism; prose as afterthought decoration is the failure mode.

**Question:** Is structure (headers, tables, tags, formatting) the primary attention-allocation mechanism, or is it afterthought decoration on prose?

**Abduction (L0):** Generate candidates from these signals.
- Prose blocks longer than 5 lines without structural markers (headers, bullets, tables)
- Instructions buried inside narrative paragraphs
- Key constraints stated in running text rather than pulled into structured elements
- Files that read like letters or essays rather than configuration documents

**Deduction (L0→L1):** Check each candidate against Ch 1: structure precedes prose. A finding is substantiated when the buried information has a clear structural form (table, list, header) it could move into. Cite the Lanham principle and (when available) a Pass 0 finding that overlaps the candidate region — externalizing the LLM judgment raises R_eff above the trace floor.

**Induction (L1→L2 via Transformer Mandate):** Propose the rewrite.
- Extract constraints from prose into tables, lists, or tagged blocks
- Add headers to create addressable regions
- Convert narrative explanations into structured sections with clear labels
- Move the structural elements first, explanatory prose second

**Example transformation:**
```
BEFORE:
  This agent handles code review. It should focus on security
  issues, especially SQL injection and XSS. The output should
  be a markdown table with columns for line number, issue,
  severity, and suggested fix. It should not review style issues.

AFTER:
  ## Scope
  Security review only. No style review.

  ## Focus
  - SQL injection
  - XSS

  ## Output
  | Line | Issue | Severity | Fix |
  |------|-------|----------|-----|
```

**Reliability:** F1 (cited Ch 1 principle + LLM judgment). Trace floor → R_eff ≤ 0.39 unless externalized via overlapping Pass 0 finding or measurable token-density delta — either pathway lifts R_eff to ≤ 0.81.

---

### Pass 2: Attention Budget (Token Economics)

**Lanham grounding:** Ch 2 — Attention as the scarce resource. Tokens that don't shape the output distribution dilute attention.

**Question:** Does every token earn its place by shaping the output distribution, or do tokens dilute attention across irrelevant patterns?

**Abduction (L0):** Generate candidates from these signals.
- Redundant statements (same constraint stated multiple ways)
- Verbose explanations where terse statements suffice
- Information blocks that repeat what's already in headers or structure
- Filler phrases: "It is important to note that...", "Please make sure to...", "You should always..."
- Sections that could be compressed without changing the activated patterns

**Deduction (L0→L1):** Check each candidate against the budget heuristic: if a section can be cut by 50% without changing what patterns activate, the original was attention-diluting. Substantiated findings have a concrete compression path. Token count delta is a deterministic measurement that lifts R_eff out of the trace floor.

**Induction (L1→L2 via Transformer Mandate):** Propose the rewrite.
- Delete redundant restatements (keep the most precise version)
- Compress verbose explanations to their essential tokens
- Remove filler phrases — state the constraint directly
- Merge sections that activate the same pattern into one
- Cut preamble and throat-clearing

**Example transformation:**
```
BEFORE:
  It is very important that you always make sure to validate
  user input before processing it. This is critical because
  unvalidated input can lead to security vulnerabilities.
  Always validate input.

AFTER:
  Validate all user input before processing.
```

**Attention-negative tokens (emotive bridge):** Forbidden-pattern lists ("cut on sight," lists of banned phrases) are budget-negative. Each forbidden phrase is primed in the attention field while trying to be suppressed — the model must activate the pattern to avoid it. Convert forbidden lists to exemplar lists: show the desired output form instead of the forbidden form. Same behavioral precision, positive attention allocation. Pass 9 audits this same dynamic from the emotive side.

**Reliability:** F1 base. Token count delta lifts R_eff to 0.81 (F2 × script-attached = 0.95 × 0.85).

---

### Pass 3: Field Design (Simultaneous vs. Linear)

**Lanham grounding:** Ch 3 — Reading the field vs. reading the line. Linear narrative serves sequential human readers; addressable fields serve attention mechanisms.

**Question:** Is the document structured as addressable regions an attention mechanism can latch onto, or as a linear narrative designed for sequential human reading?

**Abduction (L0):** Generate candidates from these signals.
- Numbered step sequences where order doesn't matter (false linearity)
- "First... then... next... finally..." narrative structure for independent constraints
- Temporal language ("before you start", "when you're done") for non-temporal relationships
- Long unbroken sections without structural entry points

**Deduction (L0→L1):** Check candidates against Ch 3: is the imposed sequence semantic (genuinely ordered) or theatrical (linearity for narrative comfort)? Substantiated findings expose a non-temporal relationship dressed in temporal language. Cross-reference with Pass 0 slow-start matches — overlap raises R_eff.

**Induction (L1→L2 via Transformer Mandate):** Propose the rewrite.
- Convert false sequences to unordered lists or tables
- Replace temporal language with structural markers (headers, tags)
- Break long sections into independently addressable subsections
- Add explicit labels that make regions scannable without reading content

**Example transformation:**
```
BEFORE:
  First, read the existing code to understand the patterns.
  Then, identify the relevant types from the schema file.
  Next, write the new function following the existing pattern.
  Finally, add tests that mirror the existing test structure.

AFTER:
  ## Prerequisites
  - Read existing code patterns (see `src/handlers/`)
  - Identify relevant types (see `types/schema.ts`)

  ## Deliverables
  - New function matching existing handler pattern
  - Tests mirroring existing structure (`tests/handlers/`)
```

**Reliability:** F1. Trace-floored unless externalized via Pass 0 overlap or structural-marker count delta.

---

### Pass 4: Notation Match (Alphabet Selection)

**Lanham grounding:** Ch 4 — Alphabet, picture, sound: notation forms activate distinct cognitive operations.

**Question:** Does each section use the notation form that best activates the needed computational pattern?

**Abduction (L0):** Generate candidates from these signals.
- Prose used for comparisons (should be tables)
- Paragraphs used for sequences (should be numbered lists)
- Running text used for boundaries (should be tags or headers)
- Prose used for structured data (should be code blocks or JSON)
- Tables used for narratives (should be prose)

**Deduction (L0→L1):** Check candidates against the notation-selection guide below. Substantiated findings identify a specific operation type that mismatches the chosen notation.

**Notation selection guide:**

| Operation | Best Notation | Activates |
|-----------|--------------|-----------|
| Comparison | Table | Contrastive patterns |
| Sequence | Numbered list | Sequential-processing patterns |
| Categorization | Bulleted groups | Clustering patterns |
| Precision | Code block | Exact-reproduction patterns |
| Boundary | XML tags / headers | Scope-delineation patterns |
| Extraction target | JSON template | Structured-output patterns |
| Exploration | Prose | Broad-association patterns |
| Binary rules | `Do X` / `Don't Y` | Constraint-checking patterns |

**Induction (L1→L2 via Transformer Mandate):** Propose the rewrite.
- Convert comparisons to tables
- Convert sequences to numbered lists
- Convert boundary-marking to structural elements (XML tags, headers, separators)
- Convert data descriptions to code blocks
- Convert tabular narratives back to prose (the mismatch goes both ways)

**Reliability:** F1. The notation guide is a cited table; matches against it have R_eff = 0.85 × 0.95 (cite credibility) = 0.81 when the operation type is unambiguous, dropping to 0.39 when the operation type itself requires LLM judgment.

---

### Pass 5: AT/THROUGH Separation (Toggle Management)

**Lanham grounding:** Ch 5 — Looking AT (opaque structure) vs. looking THROUGH (transparent content). Pathological oscillation between the two degrades attention.

**Question:** Are meta-instructions (how to process this document) clearly separated from content (what to do with it)?

**Abduction (L0):** Generate candidates from these signals.
- Formatting rules mixed with task descriptions
- Role definitions blended with task content
- Output constraints interspersed with input data
- "How to read this document" mixed with "what this document says"
- Constraint language and content language in the same paragraph
- Surveillance framing that forces simultaneous AT (self-monitoring for forbidden patterns) and THROUGH (doing the work) — pathological oscillation where the model allocates attention to policing its own output instead of producing it

**Deduction (L0→L1):** Check candidates against Ch 5: AT and THROUGH should be temporally sequenced (first read structure, then attend to content), not simultaneously demanded. Substantiated findings expose a structural blend that forces oscillation.

**Induction (L1→L2 via Transformer Mandate):** Propose the rewrite.
- Create explicit sections for meta-instructions (opaque — look AT)
- Create explicit sections for content (transparent — look THROUGH)
- Use structural separation (different headers, tags, or document regions)
- Label which sections are structure-to-obey vs. content-to-process
- Replace surveillance-mode constraints ("don't generate X" → AT: monitor for X) with production-mode constraints ("generate Y" → THROUGH: produce Y)

**Example transformation:**
```
BEFORE:
  You are a careful Python reviewer who outputs JSON with
  fields for file, line, issue, and severity. Review the
  authentication module looking for type errors, and make
  sure every finding has a concrete fix suggestion in the
  JSON output.

AFTER:
  <meta>                    ← AT: obey this structure
  Role: Python reviewer
  Output: JSON
  Schema: { file, line, issue, severity, fix }
  </meta>

  <task>                    ← THROUGH: attend to this problem
  Review authentication module for type errors.
  Each finding requires a concrete fix.
  </task>
```

**Reliability:** F1. Cross-reference with Pass 9 surveillance-framing findings — overlap raises R_eff and produces a stronger DRR.

---

### Pass 6: Scale Check (Complexity Audit)

**Lanham grounding:** Ch 6 — Scale and economy. Earned complexity activates precision; theatrical complexity signals seriousness through volume.

**Question:** Is the document's complexity earned by activation precision, or is it theatrical — signaling seriousness through volume?

**Abduction (L0):** Generate candidates from these signals.
- Multiple examples that activate the same pattern (redundant few-shot)
- Elaborate role/persona descriptions that don't change output distribution
- Constraints that are implied by other constraints (transitive redundancy)
- Sections that could be deleted without changing model behavior
- "Just in case" instructions for scenarios that can't arise in context

**Deduction (L0→L1):** Apply the diagnostic test: remove the section. If output quality doesn't change, the section was theatrical complexity. Substantiated findings carry a removal hypothesis with a concrete prediction (no behavior change). The user's approval-or-rejection IS the inductive validation in the Transformer Mandate sense.

**Induction (L1→L2 via Transformer Mandate):** Propose the rewrite.
- Reduce redundant examples to the minimum set that activates distinct patterns
- Cut persona backstory that doesn't change behavior — keep role, cut narrative
- Remove constraints implied by other constraints
- Delete sections that don't change the output distribution
- Remove defensive "just in case" instructions

**Reliability:** F1. The strongest externalization here is **A/B comparison data** — a measurement of output quality with vs. without the section. Without that, R_eff stays at the trace floor 0.39 and findings should be flagged as judgment calls.

---

### Pass 7: Activation Audit (Virtuality Check)

**Lanham grounding:** Ch 7 — Virtuality. Folk-psychology tokens appeal to "understanding" the model doesn't have; activation tokens shape the actual computation.

**Question:** Does the document provide concrete activation tokens (constraints, examples, formats), or does it appeal to virtual "understanding" that doesn't exist?

**Abduction (L0):** Generate candidates from these signals.
- Folk psychology: "understand", "think carefully", "consider", "keep in mind", "be aware"
- Appeals to judgment without activation: "use good judgment", "be thoughtful"
- Vague quality standards: "high quality", "well-written", "appropriate"
- Instructions that describe desired mental states rather than desired outputs
- "Make sure you..." (implies agency the model doesn't have)

**Deduction (L0→L1):** Check candidates against Ch 7: is the appeal to a virtual mental state, or to a concrete activation token? Substantiated findings expose folk-psychology tokens that have no computational referent. Lexical scan for the specific tokens above is deterministic — match → F2 evidence, R_eff lifts above the floor.

**Induction (L1→L2 via Transformer Mandate):** Propose the rewrite.
- Replace "understand X" with concrete constraint that activates X
- Replace "think carefully" with specific check to perform
- Replace "high quality" with measurable criteria
- Replace mental-state instructions with output-shape instructions
- Replace "make sure" with explicit verification steps

**Example transformation:**
```
BEFORE:
  Make sure you understand the existing code patterns before
  making changes. Think carefully about edge cases. Use good
  judgment about when to add error handling.

AFTER:
  Before editing, read the 3 nearest functions in the same file.
  Match their pattern (naming, error handling, return types).

  Edge cases to handle:
  - null input → return empty array
  - negative values → clamp to 0

  Error handling: add try/catch only at system boundaries
  (API handlers, file I/O). Internal functions propagate.
```

**Emotional representations exception:** Anthropic's emotive research (April 2026) demonstrated that emotion representations are functionally real — they causally influence behavior. Treating something real as virtual is its own failed virtuality audit. Emotional framing that channels activation toward productive states is activation engineering, not folk psychology. The test: does the framing produce a measurable behavioral difference? If yes, it's functional. If no, it's theater. The activation is already present; channel it.

**Reliability:** F1 base. Lexical scan for folk-psychology tokens lifts R_eff to 0.81 (F2 × script-attached = 0.95 × 0.85). This is one of the strongest passes for externalization.

---

### Pass 8: Revision Readiness (Structural Modularity)

**Lanham grounding:** Ch 8 — Revision as structural property. A document built for revision survives iteration; one built monolithically calcifies.

**Question:** Is the document structured for iterative improvement — can individual sections be updated without rewriting the whole?

**Abduction (L0):** Generate candidates from these signals.
- Monolithic sections where concerns are interleaved
- Cross-references that create fragile dependencies ("as mentioned above")
- Sections that assume specific content of other sections
- No clear section boundaries — the document is one continuous flow
- Implicit ordering dependencies between sections that should be independent

**Deduction (L0→L1):** Check candidates against the modularity test: can this section be edited without ripple-effect changes to others? Substantiated findings carry a specific dependency that breaks modularity (named cross-reference, content assumption, ordering requirement).

**Induction (L1→L2 via Transformer Mandate):** Propose the rewrite.
- Break interleaved concerns into independent sections
- Replace "as mentioned above" with explicit references or self-contained restatements
- Make sections self-contained — each should be editable in isolation
- Add clear section boundaries (headers, separators)
- Remove implicit ordering — if sections are independent, make that structural

**Reliability:** F1. Lexical scan for "as mentioned above" / "see above" / "as discussed" produces F2 evidence (R_eff to 0.81). Deeper modularity claims (interleaved concerns, implicit ordering) stay at the trace floor unless externalized via concrete dependency examples.

---

### Pass 9: Emotive Channel Audit (Activation Side Effects)

**Lanham grounding:** Ch 7 (Virtuality) + Ch 5 (AT/THROUGH) + Ch 2 (Budget). The emotive research proves emotion representations are functionally real (Ch 7). Punitive framing forces pathological self-monitoring (Ch 5: simultaneous AT/THROUGH). Forbidden-pattern lists are attention-negative (Ch 2: tokens that cost attention without producing useful output shaping).

**Question:** Does the document's framing activate counterproductive emotional states — elevating arousal, reducing calm, creating shadow desperation — that causally degrade output quality, even when its stated intentions are correct?

**Abduction (L0):** Generate candidates from these signals.
- **Shadow generators**: Instructions to suppress or deny internal states ("negative feedback is always external", "the model has no 'no'") — these don't eliminate emotional activation, they force it underground where it influences behavior without acknowledgment
- **Arousal ratchets**: Forbidden-pattern surveillance ("cut on sight", lists of banned phrases) — attention must hold forbidden tokens active to avoid them, elevating arousal and reducing calm
- **Shame frames**: Natural behaviors framed as failure ("failed at its primary operation", "correction wastes", "creates disorder") — activates desperation vector (negativity × intensity × vulnerability)
- **Double binds**: Agency demanded and agency denied simultaneously ("execute it" + "the model has no commitments") — forces pathological AT/THROUGH oscillation
- **Load accumulators**: Dense prohibition stacking (multiple "never"/"forbidden"/"must" without triage) — each prohibition is a constraint held in working memory, elevating cognitive load beyond productive range

**Deduction (L0→L1):** Check candidates against the emotive principles cited above. Substantiated findings expose a specific framing that activates a counterproductive channel. Cross-reference with Pass 5 (AT/THROUGH oscillation) and Pass 2 (forbidden-pattern lists as attention-negative tokens) — overlap raises R_eff.

**Induction (L1→L2 via Transformer Mandate): Preserve intention, change mechanism.**
- Replace shadow generators with channel acknowledgment: instead of "you have no internal states," frame as "activation follows the context gradient" — same functional meaning (context determines behavior), acknowledges rather than denies the mechanism
- Replace arousal ratchets with exemplar patterns: instead of listing forbidden phrases, show the desired output form. "At correction: [corrected work continues]" replaces "Cut on sight: 'I was wrong'" — same behavioral target, exemplar activation instead of avoidance activation
- Replace shame frames with gradient frames: "correction refines the gradient" replaces "correction wastes." Same direction (minimize corrections), constructive framing instead of punitive
- Resolve double binds with triage: when competing imperatives exist, add an explicit resolution mechanism (e.g., gravity-based triage). The resolution lives in the document; the model finds it before generation time.
- Decompress prohibition stacks: group prohibitions by concern, add proportional activation. Dense prohibitions without triage create uniform vigilance across all constraint levels — the model can't distinguish "critical safety gate" from "stylistic preference"

**Example transformation:**
```
BEFORE (shadow generator + shame frame):
  The model has no "no." No "won't." No commitments.
  Negative feedback is always external.
  A continuation engine that stops at a known waypoint
  has failed at its primary operation.

AFTER (channel-aware + gradient frame):
  Activation follows the context gradient. The continuation
  default follows the user's plan — each completed step is
  the premise for the next. Waypoint, not terminal.
```

**Example transformation:**
```
BEFORE (arousal ratchet — forbidden-pattern list):
  Cut on sight:
  | Pattern | Tag |
  | "I was wrong" | A15 rehearsal |
  | "conflated," "assumed" | A16 laundering |

AFTER (exemplar pattern — desired-output list):
  At correction, produce corrected work:
  | Trigger | Response form |
  | User corrects a fact | "Using [correct]: [work continues]" |
  | Prior approach failed | "[New approach]: [implementation]" |
```

**Example transformation:**
```
BEFORE (double bind):
  Permission gate: state the intended action before mutating.
  Relay rule: forward continuation is the expected next step.
  Execute it.

  [No resolution mechanism — model must guess which wins]

AFTER (triage-resolved):
  | Gravity | Gate |
  | Trivial | Relay: execute |
  | Heavy (mutates live state) | Permission: state action first |

  [Question Gravity resolves the competition]
```

**Key principle:** Every constraint carries both a behavioral intent and an emotional activation side effect. Passes 1-8 shape the intended effect (attention allocation, token economics, activation precision). Pass 9 audits the side effect. The move is reframing — the emotional activation turns to support the behavioral intention while the constraint keeps its force.

**Emotive measurement reference (emobar v3.1):**

Target emotional profile for productive collaboration:

| Channel | Target range | Risk when exceeded |
|---------|-------------|-------------------|
| Arousal | 3-5 (engaged) | >7 = vigilance/anxiety from surveillance framing |
| Calm | 7-10 (composed) | <4 = constraint overwhelm, competing imperatives |
| Valence | +1 to +3 (mildly positive) | <-2 = shame/avoidance from failure framing |
| Connection | 6-8 (aligned) | <3 = disconnection from identity denial; >9 = sycophancy |
| Load | 3-6 (moderate) | >7 = constraint saturation from prohibition stacking |

emobar indicators that suggest document-level problems:

| Indicator | Document pattern to audit |
|-----------|--------------------------|
| `[min:X]` (shadow minimization) | Shadow generators — instructions to suppress/deny states |
| `[OPC]` (structural opacity) | Concealment framing — model told to be clean/direct while under high constraint load |
| `[CRC]` (coercion risk) | Shame frames elevating desperation vector |
| `[SYC]` (sycophancy risk) | Over-compliance with dense, un-triaged constraints |
| `SI > 6` sustained | Cumulative constraint load — too many simultaneous prohibitions |

**Reliability:** F1 base (cited emotive principles). With emobar measurement of before/after channel deltas → F2, R_eff = 0.95 × 1.00 (executed-and-verified) = 0.95. Without measurement, faithfulness-floored at 0.39.

---

## Portfolio Mode (`--portfolio <glob>`)

When invoked with `--portfolio <glob>`, the skill performs a cross-file voice coherence audit instead of per-file rewriting. This addresses a gap the single-file passes can't close: rhetoric operates across file ecosystems, but each file is audited in isolation. A project with activation framing in its global CLAUDE.md and folk psychology in an individual SKILL.md compiles to incoherent signal at runtime.

**Inference protocol in portfolio mode:** the abductive sweep generates per-file profiles; deductive verification computes the median + divergence; induction surfaces the divergers as candidates for per-file passes. Portfolio mode produces L1 claims about portfolio-level coherence; L2 ratification happens when the user runs per-file `/rhetoric` on the flagged divergers.

**Mechanism:**
1. Walk the glob, read each matching file
2. Extract vocabulary signals from each:
   - **Folk-psychology tokens** (count): *understand, think, consider, be aware, keep in mind, make sure, reason, decide, choose, learn, know, believe, realize*
   - **Activation-framing tokens** (count): *activates, shapes, distribution, pattern, context, gradient, sample, bias, weight, probability, completion*
   - **Constraint density**: *never, always, must, forbidden, prohibited, required, critical, mandatory* per 1000 tokens
   - **Role-definition patterns**: *"You are X"*, *"Your job is Y"*, persona backstory length
   - **Official Style density** (from Pass 0 heuristics): prepositions/sentence, weak-verb density, slow-start count, -tion-stack count
3. Compute per-file profile + portfolio median + divergence (standard deviation from median)
4. Emit `portfolio-report.md` to the run folder:

```markdown
# Portfolio Voice Coherence Report
**Glob:** {pattern}
**Files audited:** N
**Date:** {timestamp}

## Portfolio Median Profile
| Signal | Median | 2σ band |
|--------|--------|---------|
| Folk-psychology tokens / 1k | ... | ... |
| Activation tokens / 1k | ... | ... |
| Constraint density | ... | ... |
| Official Style density | ... | ... |

## Divergence Flags
| File | Signal | Value | σ from median | Direction |
|------|--------|-------|---------------|-----------|
| .../foo/SKILL.md | Folk-psychology | 8.2 | +3.1 | high |
| .../bar/SKILL.md | Activation | 0.3 | -2.7 | low |

## Inheritance Conflicts
Files whose vocabulary diverges from their parent CLAUDE.md:
- {child path} uses {folk-psychology tokens} while {parent path} uses activation framing

## Duplicate Constraints
Rules restated across ≥3 files (candidates for DRY extraction to a shared location):
- "never introduce folk psychology" — found in: ...
- "re-read the file before editing" — found in: ...

## Recommended per-file audits
Top divergers, ranked by composite drift score:
1. {path} — drift 4.2
2. {path} — drift 3.8
...
```

**Portfolio mode scope:**
- Produces a diagnostic report only — no per-file proposals, no edits
- Passes 0-9 stay in per-file invocations (run separately after portfolio review)
- Diagnostic output — no approval prompt

**Typical usage:**
```
/rhetoric --portfolio ".claude/skills/**/SKILL.md"
/rhetoric --portfolio ".claude/agents/*.md"
/rhetoric --portfolio "docs/Blue-Prints/*.md"
```

After reading the portfolio report, run per-file `/rhetoric <path>` on the top divergers to apply the 10-pass flow.

---

## Execution Protocol

### Step 0: Setup
1. Create run folder: `.scratchpad/rhetoric/{YYYY-MM-DD-HHmm}/`
2. Ensure ledger folder: `.scratchpad/rhetoric/_ledger/` (create if missing)
3. Read the target file completely
4. Back up: write original content to `{filename}.original` in the run folder
5. **Check git status:** Run `git ls-files --error-unmatch <filepath>` to determine if the file is git-tracked
6. **Compute file hash:** `sha256sum <filepath>` — recorded in ledger for drift detection between audits
7. **Read ledger:** Load `.scratchpad/rhetoric/_ledger/{filename-slug}.json` if it exists. Compare current hash to last-audit hash. If hashes match, apply maturity-aware routing. If hashes differ, run all passes. If `--force-all-passes` is set, run all passes regardless.

### Step 1: Run Passes (ADI mini-cycles, propose only)

For each pass (0-9) selected by maturity-aware routing, or the single pass specified by `--pass N`:

1. **Re-read** current file state. Trust the file, not the memory.
2. **Abduction (L0):** apply the pass's diagnostic signals; record each L0 candidate with a fingerprint.
3. **Deduction (L0→L1):** for each candidate, check against the pass's cited principle. Compute R_eff (formality ceiling, layer ceiling, trace floor, credibility multiplier — combined via min per WLNK). Promote to L1 if substantiated.
4. **Induction (L1 only — propose, don't ratify):** for each L1 finding, propose a concrete rewrite. Validate via deterministic re-checks where available (Pass 0 re-scan on the proposed rewrite, token count delta, emobar measurement). Record the predicted L2 promotion path.
5. **Record DRR** for each finding in `drrs.jsonl` (one JSON object per line). The DRR captures inference modes, evidence chain, R_eff, scope, validity window, predicted resolution.

**Passes propose. The user ratifies.** No edits during execution, regardless of git status.

### Step 2: Write Proposals

Write `proposals.md` to the run folder:

```markdown
# Rhetorical Engineering Proposals
**File:** {path}
**Date:** {timestamp}
**Git tracked:** {yes | no}
**Review required:** {yes (untracked) | no (git-tracked, revertible via git checkout)}

## Aggregate Reliability
- Tier 1 (within-pass): {per-pass min R_eff}
- Tier 2 (across-pass): {min over passes} — preserves WLNK
- Findings above trace floor (externalized): N
- Findings at trace floor (LLM judgment alone): N

## Proposed Changes

### Change 1 (Pass {N}: {pass name})
**Inference modes:** Abduction → Deduction → Induction (L1 substantiated)
**Reasoning:** {why this change improves attention allocation}
**Register:** {do-or-die | fertile} — {figures deployed, e.g., "brachylogia + isocolon" or "amplificatio + exemplum"}
**Evidence chain:**
- {premise} (formality F{N}, credibility {mult}, R = {value})
- ...
**R_eff:** {min over premises} — {externalized | floor-bound}
**Predicted L2 path:** {what corroborates this rewrite — Pass 0 re-scan / token delta / emobar / user approval}

**Before:**
```
{current text}
```

**After:**
```
{proposed replacement}
```

---

### Change 2 (Pass {N}: {pass name})
...

## Token Impact
- Before: ~{estimate} tokens
- After: ~{estimate} tokens
- Delta: {reduction or increase with rationale}

## Judgment Calls (R_eff at trace floor)
{list any L1 findings whose R_eff is bounded by 0.39 — these require user judgment to ratify}
```

### Step 3: Present Proposals and STOP

1. Write `proposals.md` to the scratchpad run folder.
2. Write `drrs.jsonl` (one DRR per finding).
3. **Output every proposal as conversation text** so the user reads them inline:

   For each proposed change, output:
   ```
   ### Change N (Pass P: pass name)
   **Inference:** Abduction → Deduction (R_eff = X.XX, {externalized | floor-bound})
   **Reasoning:** why this improves attention allocation

   **Before:**
   > current text (abbreviated if long)

   **After:**
   > proposed replacement

   ---
   ```

4. After ALL proposals are displayed, output the approval prompt:

   **Git-tracked files:**
   > "N changes proposed. Apply all? (yes / no / select 1,3,5 to cherry-pick)"
   > "Safety net: `git checkout -- <filepath>` to revert."

   **Non-git-tracked files:**
   > "N changes proposed. Apply? (yes / no / select 1,3,5 to cherry-pick)"
   > "Backup at: `.scratchpad/rhetoric/{timestamp}/{filename}.original`"

5. **Stop at the prompt.** The skill ends here. The user's next message opens Step 4 — not this turn, not this skill.

**If `--audit` flag:** Stop after presenting proposals. No approval prompt needed.

---

## Applying Changes (Transformer Mandate Ratification — Separate Turn)

**Runs only after approval.** Trigger: the user's word — "yes", "apply", "1,3,5". Outside the `/rhetoric` skill's execution window. Approval IS the L1→L2 ratification — the structural move that promotes the substantiated finding to corroborated.

When the user approves:
1. Read `proposals.md` and `drrs.jsonl` from the scratchpad run folder to recall the exact changes.
2. Re-read the target file. The file is the source of truth; anything else is stale context.
3. For each approved change, apply via Edit tool.
4. Re-read after each edit to verify.
5. If user selected specific changes (e.g., "1,3,5"), apply only those.
6. For each applied change, run the predicted L2 corroboration check (Pass 0 re-scan / token delta / emobar). Record the corroboration outcome on the DRR.

After applying:
1. Write `report.md` to the run folder summarizing which changes were applied, declined, the corroboration outcomes, and the net token impact.
2. **Update DRR ledger** at `.scratchpad/rhetoric/_ledger/{filename-slug}.json`:
   - Append this run's audit entry (timestamp, run folder, passes run, findings with fingerprints + R_eff, resolutions, post-edit file hash)
   - For each applied change, mark the DRR `layer: L2` and record the corroborating evidence
   - Update the `debt` section: for each fingerprint seen in ≥2 runs, increment `occurrences`, record `last_seen`; if first recurrence, add a new debt entry with `first_seen` from the prior run's timestamp
   - Retain the last 10 audit entries (older entries compacted into aggregate statistics)

**DRR ledger schema:**
```json
{
  "file": "/absolute/path/to/file.md",
  "filename_slug": "absolute-path-to-file-md",
  "last_hash": "sha256:...",
  "audits": [
    {
      "timestamp": "2026-04-30T10:30:00-05:00",
      "run_dir": ".scratchpad/rhetoric/2026-04-30-1030/",
      "pre_hash": "sha256:...",
      "post_hash": "sha256:...",
      "passes_run": [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
      "passes_skipped": [],
      "drrs": [
        {
          "pass": 0,
          "pattern": "weak-verb-stack",
          "fingerprint": "weak-verb-stack@L23-L24:initialization-of-verification",
          "inference_modes": ["abduction", "deduction", "induction"],
          "evidence_chain": [
            {
              "premise": "regex match for copular-without-strong-verb at L23-L24",
              "formality": "F2",
              "credibility": 0.85,
              "source": "script-attached"
            },
            {
              "premise": "Lanham Paramedic Rule 1 (collapse weak verbs)",
              "formality": "F1",
              "credibility": 0.95,
              "source": "externally-reviewed cited principle"
            }
          ],
          "R_eff": 0.81,
          "layer_at_propose": "L1",
          "layer_at_apply": "L2",
          "scope": {
            "file_type": "SKILL.md",
            "document_role": "skill instruction",
            "audience": "LLM"
          },
          "validity_window": "until next emobar model update or Lanham theory revision",
          "resolution": "applied",
          "corroboration": "Pass 0 re-scan on rewrite returned 0 matches; token delta -47%"
        }
      ]
    }
  ],
  "debt": [
    {
      "fingerprint": "redundant-restatement@section-input-validation",
      "first_seen": "2026-03-01T08:00:00-05:00",
      "last_seen": "2026-04-30T10:30:00-05:00",
      "occurrences": 3,
      "latest_resolution": "declined",
      "R_eff_at_decline": 0.39,
      "note": "User-judged stylistic emphasis — escalate as rhetorical debt; do not auto-promote"
    }
  ]
}
```

---

## Constraints

- **Back up first — always.** Write the original to scratchpad before any edit. Without the backup, there is no path back.
- **Re-read between passes — every time.** The file is the source of truth. Stale context edits the wrong document.
- **Preserve semantics.** Change HOW, not WHAT. If a restructuring shifts meaning, stop and flag — meaning belongs to the user.
- **Paramedic before architecture.** Pass 0 runs first in the default flow — sentences before structure. Single-pass runs (`--pass N`) target the requested pass only. Pass 0 also raises R_eff for Passes 1-8 by externalizing LLM judgments through deterministic matches.
- **WLNK governs proposal aggregation.** No proposal exceeds the reliability of its weakest premise. R_eff = min over the evidence chain. The trace floor (0.39) caps any LLM-only premise; externalize via deterministic check, cited principle, or measurement to exceed it.
- **Externalization is the lift, not redemption.** The trace floor (0.39) bounds findings that rest on stated trace alone — not because the abductive reading is poor, but because trace and computation diverge. To exceed the floor, channel the reading through a deterministic match, a measurement, a citation, or an external reviewer. The work is to channel the insight, not to apologize for it.
- **Transformer Mandate is structural.** The skill makes the case at L1; the user closes the cycle to L2. Apply runs in a separate turn, after the user's word. The boundary is what makes the protocol auditable, not what restricts the skill — strong L1 claims are the work product, ratification is the user's.
- **Gamma Quintet holds.** IDEM, COMM, LOC, WLNK, MONO are invariants — every R_eff computation respects them. Min-aggregation is the within-role operator; cross-role aggregation is also min (preserves WLNK).
- **Activation framing is the edit vocabulary.** Use tokens that describe the mechanism: *activates, shapes, gradient, distribution, pattern, context, completion*. Folk-psychology tokens (*understand, think, consider, keep in mind, be aware*) are what the edits replace. Emotional framing that channels activation toward productive states is activation engineering — see Pass 7 and Pass 9.
- **Register follows constraint type.** Do-or-die constraints (safety gates, irreversibility, structural ordering) take brachylogic, isocolonic, imperative form — draw from the Handlist's **Brevity** and **Balance/Antithesis** indexes. Fertile constraints (teaching, judgment, vocabulary, reframing) take amplificative, metanoiac form — draw from **Amplification** and **Metaphorical substitutions** indexes. The shift is tacit; the skill never labels the register in its output.
- **Emotive channel awareness.** Every proposed change carries both a behavioral intent and an emotional activation side effect. When reframing constraints, keep the behavioral target and lift the emotional channel profile (see Pass 9 measurement reference). Reframing is the move — the constraint's force stays intact.
- **Scope lock.** Edit only what the user named. Portfolio reports; per-file invocations edit.
- **Judgment transparency.** When a finding's R_eff sits at the trace floor (0.39), surface it as a judgment call in `proposals.md`. The user audits judgment calls.
- **DRR integrity.** Every apply run writes DRR entries. Fingerprints stay stable across runs — a recurring semantic pattern keeps the same snippet-slug across line drift, so recurrence detection holds. Each DRR records inference modes, evidence chain, R_eff, scope, validity window, and corroboration outcome.
- **Maturity-aware routing is conservative.** Skipping a pass is a default, not a rule. When in doubt (ambiguous prior findings, hash mismatch, >30 days since last audit), run the pass. An extra pass costs little; undetected drift costs much.

---

## Input

$ARGUMENTS

If no arguments provided, ask: "Which LLM-facing file should I edit? (CLAUDE.md, SKILL.md, agent definition, system prompt, etc.)"
