# kiki-c0/skills — repo context for Claude Code

A two-track skills repo published to the Claude Code marketplace.

## Layout

- `./disciplines/` — unsolved-for-Claude disciplines, human-facing. Each entry: `README.md` (authoritative), `SPEC.md`, `evals/evals.json`, `.claude-plugin/plugin.json`. **No `SKILL.md`** — intentional silent-no-op filter.
- `./claude/skills/` — functional Claude skills (or stubs targeting one). `SKILL.md` when ready; `SPEC.md` always; `evals/` optional.
- `./.claude/commands/` — Claude Code slash commands, auto-discovered when the repo is opened in Claude Code.
- `./.claude/settings.json` — tracked Claude Code permission defaults (allow read-only ops, ask for remote writes, deny force-push to main / `gh pr merge` / `gh repo delete`).
- `./.claude-plugin/marketplace.json` — marketplace manifest. Only ship-ready plugins listed.

## Conventions

- **Markdown prose: soft-wrap.** One paragraph per line. Do not hard-wrap at a column width. Exception: commit message bodies wrap at ~72.
- **Silent-no-op design.** Adding a `SKILL.md` under `disciplines/` breaks the design — disciplines stay human-facing. If a discipline is ready for automation, scaffold it under `claude/skills/<name>/`.
- **License: MIT** in `plugin.json`. No `LICENSE` file yet.
- **Versioning:** `0.1.0` for pre-eval-validated skills, bump to `1.0.0` once evals pass.
- **No `Co-Authored-By: Claude` footers** in commits.

## Schemas

`marketplace.json`:

```json
{
  "name": "<kebab>",
  "owner": { "name": "<string>" },
  "plugins": [
    { "name": "<kebab>", "source": "./<path>", "description": "<string>", "version": "<semver>" }
  ]
}
```

`plugin.json` (per-plugin, at `<plugin>/.claude-plugin/plugin.json`):

```json
{
  "name": "<kebab>",
  "version": "<semver>",
  "description": "<string>",
  "author": { "name": "<string>" },
  "license": "<spdx>"
}
```

`evals.json`:

```json
{
  "skill_name": "<kebab>",
  "evals": [
    { "id": 1, "name": "<kebab>", "prompt": "<string>", "expected_output": "<string>", "files": [] }
  ]
}
```

## Adding content

- **New discipline:** `disciplines/<name>/{README.md, SPEC.md, evals/evals.json, .claude-plugin/plugin.json}`. Append an entry to `.claude-plugin/marketplace.json`. Update the top-level `README.md` "Available skills" section.
- **New Claude skill:** `claude/skills/<name>/{SPEC.md[, SKILL.md, evals/evals.json, .claude-plugin/plugin.json]}`. List in marketplace only when `SKILL.md` ships.
- **New command:** `.claude/commands/<name>.md` with YAML frontmatter (`description`, `argument-hint`, `allowed-tools`).
- **New eval case for scrutiny:** use the `/add-scrutiny-eval` command.

## PR workflow

- `main` is protected: require PR, 1 approval, no force-push, no deletion, conversation resolution required. Admin bypass enabled for the owner.
- For orphan-branch rewrites, merge with `-s ours` first so `main` becomes an ancestor (precedent: PR #1).
- Commit subjects: lowercase, imperative, scoped with `<area>:` when useful.
- Commit bodies: explain WHY.

## When Claude Code runs via the PR review workflow

Scope: only review changes under `./claude/` and `./.claude/`. Do not review `./disciplines/` — those are human-authored artifacts outside the automated review surface.

Use this file as the spec for what conventions the PR must follow. Post inline comments on specific problematic lines. Leave a summary review. Be specific and cite the convention each flagged issue violates. Don't re-review unchanged parts of the file.
