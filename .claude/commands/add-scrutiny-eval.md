---
description: Capture a new scrutiny eval case from a suspicious claim you encountered in analytical writing, and append it to disciplines/scrutiny/evals/evals.json.
argument-hint: [optional — paste the offending claim, or run without args for a guided walkthrough]
allowed-tools: Read, Edit, Write, Bash
---

You are helping the user capture a new eval case for the `scrutiny` discipline. The eval file lives at `disciplines/scrutiny/evals/evals.json`.

## Workflow

1. Read `disciplines/scrutiny/README.md` for the discipline and `disciplines/scrutiny/evals/evals.json` for the existing case style and schema.
2. If `$ARGUMENTS` is empty, ask the user:
   - What claim did Claude make that felt weak? Paste the sentence or short passage.
   - What audit *should* have happened? Which of the three tests (example-survival, uniqueness, falsifiability) does the claim fail? What verdict should the scrutineer produce?
3. Draft a new eval entry matching the schema of existing cases:
   - `id`: next integer after the current max.
   - `name`: kebab-case, descriptive (e.g., `overreach-on-adjective`, `list-with-mixed-claims`).
   - `prompt`: the scenario as a reviewer would present it to Claude. Usually `"Review this passage..."` + the claim.
   - `expected_output`: the audit you'd expect a scrutineer to produce. Specific verdict. Name the failing test. Match the terseness of the existing cases.
   - `files`: `[]` unless the case needs attached files.
4. Show the user the drafted entry. Iterate until they approve.
5. Append to `disciplines/scrutiny/evals/evals.json`. Preserve JSON formatting; add the comma on the previous last entry.
6. Remind the user to commit and, if they're working from a fork, open a PR back to `kiki-c0/skills`.

## Tone

This is a contribution workflow, not a generation task. Defer to the user on the audit content — do not invent scrutiny verdicts. Draft what they describe, refine until they're satisfied. If their audit itself looks weak (e.g., a verdict that doesn't name the failing test), mention that as scrutiny applied to the eval itself — but let them decide whether to refine it or ship it.
