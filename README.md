# kiki-c0/skills

A skills repo with two tracks:

- `./disciplines/` — unsolved-for-Claude disciplines, shipped as human-facing collateral (README + SPEC + evals). No `SKILL.md`, by design.
- `./claude/skills/` — functional Claude skills, or stubs targeting a future functional version.

## Available skills

- [scrutiny](disciplines/scrutiny/README.md) — pressure-test load-bearing claims in analytical writing.

## Forking this repo

Got an idea for making one of the unsolved disciplines actually work inside Claude's default cognitive mode? Fork and try. Each entry in `./disciplines/` ships with:

- `README.md` — the discipline for humans (authoritative).
- `SPEC.md` — what a Claude-facing version would require, and why prior attempts didn't earn their keep.
- `evals/` — test cases drawn from real sessions. These are the bar: does your version reproduce what the human scrutineer did manually?

Reasonable directions:

- Run the evals against the current collateral; report the failure modes.
- Add a `SKILL.md` with a prompt-only hypothesis; rerun evals.
- Build tool-use scaffolding per `SPEC.md`; rerun evals.

PRs welcome. Negative results are useful — if your approach didn't beat the ratification loop, the failure mode belongs in the SPEC.
