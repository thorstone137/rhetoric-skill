# Contributing

Three ways to contribute, ranked by what helps most.

## 1. Audit a real CLAUDE.md and post the findings

Run `/rhetoric` on a public `CLAUDE.md` (your own project, an OSS project's, anthropic-cookbook's). Open an issue with the title `Audit: <project>` and paste the proposals.md output. These become reference cases for the regex bank and the worked-example library.

## 2. Open issues for false positives or false negatives

Found a Pass 0 match that's wrong (matched code in a non-fenced block, matched a quotation)? Open an issue with:
- The fragment that triggered the false match
- The pass and rule that fired
- What you'd expect instead

The auto-ignore scope list (code blocks, quotations, tables, frontmatter) grows from these reports.

## 3. PR a new auto-ignore rule or a Lanham principle gap

The 10 passes cover *Economics of Attention*'s nine chapters plus the emotive layer. If you find a gap — a Lanham principle or attention-economics phenomenon the skill misses — PR it as a new pass or as additional signals under an existing pass.

PR checklist:
- [ ] New rule or pass cites the source (Lanham chapter + page, Anthropic paper section, etc.)
- [ ] Reliability scoring follows the existing F1/F2 formality ceilings
- [ ] At least one before/after example in the pass description
- [ ] Existing tests still pass (run `/rhetoric --pass <N>` on the test corpus in `tests/`)

## Code of conduct

Be precise. Cite. Disagree with reasoning, not labels. If you're correcting a finding the skill made, write the corrected output — don't describe what should be there.

## License

Contributions are accepted under the same MIT license as the GitHub-hosted skill. Commercial-use license (separate, paid) does not affect contributor terms.
