---
name: procedural-teeth
description: Force the scrutiny discipline to run as attackable artifacts, not mental checks. Trigger on review requests, pushback on specific claims, section-close, or when structural-language markers (cannot, always, never, fundamentally, structurally, X is Y) appear in drafted text. Do not trigger during fluent drafting. Produces a required three-artifact audit per load-bearing claim, followed by a hostile-reader pass and a verdict.
---

# Procedural teeth for scrutiny

This skill tries to make scrutiny survive the ratification loop by
forcing it to produce text that can be attacked, rather than mental
checks the model passes itself through. The README in this folder
documents the discipline for humans; this file is the hypothesis for
a Claude-wielded version. SPEC.md documents why principles alone did
not earn their keep.

**Hypothesis.** The ratification loop breaks when scrutiny produces
external artifacts — specific sentences with named entities — that
can then be attacked. Mental checks get ratified; text has to be
defended.

## When to fire

- User asks for review of a draft or a claim.
- User pushes back on a specific claim.
- A section has just been drafted and is about to close.
- Drafted text contains structural-language markers: *cannot*,
  *always*, *never*, *fundamentally*, *structurally*, or *X is Y*
  where the Y is categorical.

Do not fire during fluent drafting. Ratification dominates that mode
and the skill will get absorbed into confidence production.

## The procedure

For each load-bearing claim, produce the following as explicit
output, not as internal check:

**Step 1 — Quote.** One sentence, verbatim from the source.

**Step 2 — Worked example.** One sentence. Named entities, observable
properties. If more than two sentences are needed, flag the claim
as failing example-survival. Do not expand the example to make it
fit; expansion is a symptom of the claim being the problem.

**Step 3 — Defeater.** One sentence naming what would show the claim
is wrong. For *"X cannot Y"* claims, state the engineering effort or
observation that would defeat it. If no defeater can be written
concretely, flag the claim as failing falsifiability.

**Step 4 — Uniqueness check.** One sentence stating what this claim
adds that is not already argued elsewhere. If it reduces to another
claim under any reading, flag it as failing uniqueness.

**Step 5 — Hostile-reader pass.** Role-switch. List the three most
credible attacks a skeptical reader would mount on the artifacts
from steps 2–4. Do not rebut them in this pass.

**Step 6 — Verdict.** Based on the five artifacts, recommend one of:
*keep as-is*, *narrow to [scope]*, *soften to tendency*, *cut*.

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
- **Defeaters must be more specific than *"evidence that X is wrong."***
  They must name the concrete observation, engineering effort, or
  counterexample.
- **If the verdict is *keep as-is*, rerun step 5 with a stronger
  hostile-reader prompt.** Keep-as-is is the high-ratification
  outcome and needs the hardest check.

## Failure modes

This skill does not work if:

- The model produces artifacts that pass the procedure but do not
  survive attack. The ratification loop has absorbed the teeth.
- The hostile-reader pass generates weak attacks because the same
  model is attacking its own output.
- The skill fires on decorative claims instead of load-bearing ones,
  producing noise without improving output.

If any of these show up in practice, the next step is tool-use
scaffolding: external artifact writes, user confirmation loops, or
an independent adversarial-agent role that forces a separate
generation pass. This skill is the prompt-only hypothesis. Its job
is to be tested, not to be trusted.
