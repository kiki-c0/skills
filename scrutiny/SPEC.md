# Spec: Procedural teeth for Claude-wielded scrutiny

A design note for a future SKILL.md. The README.md in this folder
documents the discipline for humans, which works now. This spec
describes what a Claude-facing version would require, and why
principles alone did not earn their keep.

## Why this is not a skill yet

Loading scrutiny principles as a skill does not reliably change
Claude's drafting behavior. The failure mode is the ratification loop:

  produce claim → produce supporting example → ratify own output → move on

Tests applied inside this loop get ratified too. The loop is stronger
than the prompt. Evidence: the conversation that produced this folder,
where scrutiny principles were articulable but did not prevent the
model from cycling through three forced examples before the human
caught the pattern.

Humans break this loop by switching into a skeptical reader mode —
meta-cognition about their own pattern-matching. Claude does not
reliably execute that switch from a prompt instruction alone.

## What procedural teeth would look like

Hypotheses, not specifications. Each addresses a different lever on
the ratification loop.

**1. Forced artifact production.**
The three tests become required writing steps, not mental checks.
For each load-bearing claim, produce:

- a one-sentence worked example with named entities,
- a one-sentence statement of what would defeat the claim,
- a one-sentence check that the claim does work other claims don't.

If any cannot be produced in under two sentences, flag the claim.
The tangible artifact creates something that can be attacked; that
is where the loop-break happens.

**2. Hostile-reader intermezzo.**
After drafting a section, an explicit mode switch: *read this as a
hostile reader; list the three most credible attacks.* Scripted,
not optional — the loop ratifies its way past optional steps.

**3. Linguistic-marker triggering.**
Fire on specific language that correlates with weak claims:

  cannot, always, never, fundamentally, structurally, X is Y

When the marker appears, the three tests run on the containing
claim. Narrows the scrutiny surface and makes the trigger observable
rather than judgment-dependent.

**4. Narrow scope.**
Do not fire during fluent drafting — that is where ratification
dominates. Fire on review, on pushback, on section-close. Contexts
where adversarial mode is already partially invited, so the skill
has traction.

## Open questions

- Can a prompt alone force artifact production, or does it require
  tool-use scaffolding (file writes, structured output)?
- Are the linguistic markers reliable, or too noisy?
- Does role-switch change the generating distribution, or does the
  same model ratify both sides of its own dialogue?
- Does the skill work on-demand, or does it require always-on hooks?

## Non-goals

- Solving alignment.
- Making Claude infallible.
- Replacing the human scrutineer. The README stays authoritative
  regardless of how good the teeth get.
- Universal rigor across all writing. This is for analytical pieces
  with load-bearing claims.

## Validation

Apply scrutiny to the teeth before deploying them:

- **Example-survival:** a specific case where the teeth caught a
  claim Claude would otherwise have ratified. The conversation that
  produced this folder is a candidate test.
- **Uniqueness:** does this add behavior the README does not already
  produce through the human? If the human is scrutineering anyway,
  the teeth are decorative.
- **Falsifiability:** name what would show the teeth do not work.
  Example: Claude ratifies through the artifact-production step by
  producing an example that looks correct but does not survive
  attack.
