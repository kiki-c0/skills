# analytic-rigor — Claude skill spec

Target Claude-facing implementation of the scrutiny discipline. Currently a stub: no `SKILL.md` means the package installs silently and never fires.

See `../../../disciplines/scrutiny/README.md` for the discipline itself (authoritative for humans). See `../../../disciplines/scrutiny/SPEC.md` for the conceptual design — why procedural teeth are needed and what they would look like.

## Scope of this spec, when drafted

Implementation-level detail the discipline's `SPEC.md` does not cover:

- **Triggers.** Which user prompts or drafting moments should fire the skill (review requests, pushback, section-close, structural-language markers). Concrete regex or semantic patterns, not just categories.
- **Outputs.** What the skill writes when it fires — the three-artifact audit, hostile-reader pass, verdict. Format and length targets.
- **Triage policy.** Concrete load-bearing vs. decorative classification rules, with worked examples in both directions. The discipline names the categories; this spec names the rules.
- **Non-triggers.** Contexts the skill must explicitly *not* fire in (technical specs, API docs, config) where structural language is routine and not analytical overreach.
- **Pushback behavior.** How the skill handles the "fresh audit" rule when challenged on one of its own audits.

## Validation

The bar lives in `../../../disciplines/scrutiny/evals/evals.json`. A `SKILL.md` is ready to ship when it reproduces the expected audits across all cases, including the negative case (decorative markers in API docs) which tests triage.

## Status

Stub. No `SKILL.md` yet. Not listed in `.claude-plugin/marketplace.json`.
