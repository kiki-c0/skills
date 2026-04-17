# Spec: Procedural teeth for Claude-wielded scrutiny

A design note for what a Claude-facing scrutiny skill would need to do, and why the prompt-only version needs empirical validation before it earns a `SKILL.md`. The README.md in this folder documents the discipline for humans, which works now. Running the evals in `evals/` is the next step.

## Why this is not a skill yet

Loading scrutiny principles as a skill does not reliably change Claude's drafting behavior. The failure mode is the ratification loop:

  produce claim → produce supporting example → ratify own output → move on

Tests applied inside this loop get ratified too. The loop is stronger than the prompt. Evidence: the conversation that produced this folder, where scrutiny principles were articulable but did not prevent the model from cycling through three forced examples before the human caught the pattern.

Humans break this loop by switching into a skeptical reader mode — meta-cognition about their own pattern-matching. Claude does not reliably execute that switch from a prompt instruction alone.

## What procedural teeth would look like

Hypotheses, not specifications. Each addresses a different lever on the ratification loop.

**1. Forced artifact production.**
The three tests become required writing steps, not mental checks. For each load-bearing claim, produce:

- a one-sentence worked example with named entities,
- a one-sentence statement of what would defeat the claim,
- a one-sentence check that the claim does work other claims don't.

If any cannot be produced in under two sentences, flag the claim. The tangible artifact creates something that can be attacked; that is where the loop-break happens.

**2. Hostile-reader intermezzo.**
After drafting a section, an explicit mode switch: *read this as a hostile reader; list the three most credible attacks.* Scripted, not optional — the loop ratifies its way past optional steps.

**3. Linguistic-marker triggering.**
Fire on specific language that correlates with weak claims:

  cannot, always, never, fundamentally, structurally, X is Y

When the marker appears, the three tests run on the containing claim. Narrows the scrutiny surface and makes the trigger observable rather than judgment-dependent.

**4. Triage-based scoping.**
Fire on claim type, not on drafting phase. Every trigger (review request, pushback, section-close, structural-language marker) runs a triage pass first: is this claim load-bearing analytical content or decorative/technical-spec language? Load-bearing runs the full procedure; decorative skips. Default to trigger on ambiguity — false-positive noise is cheaper than letting a weak claim through.

Rejected alternative: gating by drafting phase ("don't fire during fluent drafting"). That moved the weakness into the machinery instead of out of the text, and contradicted the README's rule that the discipline has to operate on everything analytical. It was also the exact anti-pattern the README warns against — architectural overreach named with structural language.

## Open questions

- Can a prompt alone force artifact production, or does it require tool-use scaffolding (file writes, structured output)?
- Are the linguistic markers reliable in analytical prose, or too noisy to be the primary trigger?
- What's the false-positive rate in technical-specification prose (API docs, type signatures, config), where "always" and "never" are routine load-bearing but not architectural? Triage is the current answer; the decorative-marker eval exercises it.

## Non-goals

- Solving alignment.
- Making Claude infallible.
- Replacing the human scrutineer. The README stays authoritative regardless of how good the teeth get.
- Universal rigor across all writing. This is for analytical pieces with load-bearing claims.

## Validation

Apply scrutiny to the teeth before deploying them.

- **Example-survival:** see `evals/evals.json` — four prompts lifted from the session that produced this folder, each with an audit the human scrutineer performed manually. The teeth work if the skill reproduces those audits.
- **Uniqueness:** does this add behavior the README does not already produce through the human? If the human is scrutineering anyway, the teeth are decorative.
- **Falsifiability:** name what would show the teeth do not work. The strongest failure mode lives in eval 2 (pushback → fresh audit): if the skill capitulates ("you're right, let me try again") instead of producing the independent verdict the human produced, prompt-only has no traction on the ratification loop and tool-use scaffolding is the next step.
