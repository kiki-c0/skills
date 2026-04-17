# kiki-c0/skills

A skills repo with two tracks:

- `./skills/` — unsolved-for-Claude disciplines, shipped as human-facing collateral (README + SPEC + evals). No `SKILL.md`, by design.
- `./claude/skills/` — functional Claude skills. Empty for now.

## Available skills

- [scrutiny](skills/scrutiny/README.md) — pressure-test load-bearing claims in analytical writing.

## Forking this repo

Got an idea for making one of the unsolved skills actually work inside Claude's default cognitive mode? Fork and try. Each skill in `./skills/` ships with:

- `README.md` — the discipline for humans (authoritative).
- `SPEC.md` — what a Claude-facing version would require, and why prior attempts didn't earn their keep.
- `evals/` — test cases drawn from real sessions. These are the bar: does your version reproduce what the human scrutineer did manually?

Reasonable directions:

- Run the evals against the current collateral; report the failure modes.
- Add a `SKILL.md` with a prompt-only hypothesis; rerun evals.
- Build tool-use scaffolding per `SPEC.md`; rerun evals.

PRs welcome. Negative results are useful — if your approach didn't beat the ratification loop, the failure mode belongs in the SPEC.
