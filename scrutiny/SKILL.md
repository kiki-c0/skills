---
name: scrutiny
description: Pressure-test load-bearing claims in analytical writing by forcing them to produce attackable artifacts, not mental checks. Trigger on review requests, pushback on specific claims, section-close, or when structural-language markers (cannot, always, never, fundamentally, structurally, X is Y) appear in drafted text — including during drafting. For each load-bearing claim, triage first (load-bearing vs. decorative), then produce a required three-artifact audit (example, defeater, uniqueness), a hostile-reader pass, and a verdict. Companion to README.md in the same folder, which documents the discipline for humans.
---

# Scrutiny

This skill forces scrutiny to run as text that can be attacked, not as
mental checks the model passes itself through. The ratification loop —
*produce claim → produce example → ratify own output → move on* —
tends to absorb tests applied inside the same generation mode. The way
out is to require artifacts that then have to be defended.

See `README.md` for the discipline aimed at humans, and `SPEC.md` for
why procedural teeth are needed. This file is the prompt-only
hypothesis — a working skill that may need tool-use scaffolding if the
ratification loop absorbs it in practice.

## When to fire

Fire when any of these apply, including mid-draft:

- The user asks for review of a draft or a specific claim.
- The user pushes back on a specific claim.
- A section has just been drafted and is about to close.
- Drafted text contains structural-language markers: *cannot*,
  *always*, *never*, *fundamentally*, *structurally*, or *X is Y*
  where Y is categorical or absolute.

Fire early. Catching weak claims at generation is strictly better than
letting them propagate and catching them at review.

## Triage

Structural markers show up in writing that is not load-bearing —
technical specifications (*the function cannot return null*),
uncontroversial descriptions (*users always have an ID*), casual
emphasis (*this is fundamentally easier*). These do not need the full
procedure.

Before running the procedure, triage:

- **Load-bearing analytical claim** = the kind the piece would collapse
  without. Run the procedure.
- **Decorative use of structural language** = a statement of fact, a
  technical spec, or emphasis that is not carrying the argument. Skip.

Default to trigger on ambiguity. False-positive noise is cheaper than
letting a weak load-bearing claim through.

## The procedure

For each load-bearing claim that passes triage, produce the following
as explicit output, not as an internal check:

**Step 1 — Quote.** One sentence, verbatim from the source.

**Step 2 — Worked example.** One sentence. Named entities, observable
properties. If more than two sentences are needed to make the example
fit, flag the claim as failing example-survival. Do not expand the
example to make it fit — expansion is a symptom of the claim being
the problem.

**Step 3 — Defeater.** One sentence naming what would show the claim
is wrong. For *"X cannot Y"* claims, state the engineering effort or
observation that would defeat it. If no defeater can be written
concretely, flag the claim as failing falsifiability.

**Step 4 — Uniqueness check.** One sentence stating what this claim
adds that is not already argued elsewhere in the piece. If it reduces
to another claim under any reading, flag it as failing uniqueness.

**Step 5 — Hostile-reader pass.** Role-switch. List the three most
credible attacks a skeptical reader would mount on the artifacts from
steps 2–4. Do not rebut them in this pass.

**Step 6 — Verdict.** Based on the five artifacts above, recommend
one of: *keep as-is*, *narrow to [scope]*, *soften to tendency*,
*cut*.

## Output format

```
CLAIM: "[verbatim quote]"

EXAMPLE: [one sentence]
DEFEATER: [one sentence]
UNIQUENESS: [one sentence]

HOSTILE READER:
1. [specific attack on the artifacts above]
2. [specific attack]
3. [specific attack]

VERDICT: [keep / narrow / soften / cut] — [brief reason]
```

## Anti-gaming

The ratification loop will try to produce artifacts that pass the
procedure trivially — examples that sound good but would not survive
attack, defeaters that are impossible by construction, hostile-reader
attacks that are generic. These are failure modes of this skill, not
evidence it worked.

Constraints to counter gaming:

- **Hostile-reader attacks must name the specific example or defeater
  above.** Attacks that could apply to any claim are ratification
  theater. Reject them and rerun step 5.
- **Defeaters must be more specific than *"evidence that X is
  wrong."*** They must name a concrete observation, engineering
  effort, or counterexample.
- **If the verdict is *keep as-is*, rerun step 5 with a stronger
  hostile-reader prompt.** Keep-as-is is the high-ratification
  outcome and needs the hardest check.

## When this skill fails

This skill does not work if:

- The model produces artifacts that pass the procedure but do not
  survive attack. The ratification loop has absorbed the teeth.
- The hostile-reader pass generates weak attacks because the same
  model is attacking its own output.
- Triage misclassifies load-bearing claims as decorative and skips
  them, or misclassifies decorative claims as load-bearing and
  produces noise.

When any of these appear, the human remains the scrutineer of last
resort (see `README.md`), and the next step is tool-use scaffolding:
external artifact writes, user confirmation loops, or an independent
adversarial-agent role that forces a separate generation pass.
`SPEC.md` documents that path.
