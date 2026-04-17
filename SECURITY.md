# Security

## Trust model

This repo ships content that Claude Code reads and, in the case of `claude/skills/` with a `SKILL.md`, auto-loads when the plugin is installed. Installing any plugin from this marketplace is an act of trust: you're letting content authored by `kiki-c0` (and reviewed through the PR process) influence your Claude Code sessions.

The `disciplines/` tree is deliberately non-firing — no `SKILL.md` — so those plugins install as silent no-ops. The `README.md`, `SPEC.md`, and `evals/evals.json` content is still read when you open the repo in Claude Code or run the evals manually. Treat all content here as you would any third-party prose.

## Reporting a vulnerability

Email `yetanotherkiki@proton.me` with:

- A description of the issue
- Steps to reproduce, or the relevant file and commit SHA
- Your assessment of impact

Please do **not** open a public GitHub issue for security reports. I'll acknowledge within 7 days.

## In scope

- Malicious or misleading content in skill or discipline files (`README.md`, `SPEC.md`, `SKILL.md`, slash commands under `.claude/commands/`).
- Prompt-injection payloads hidden in `evals/evals.json` or in markdown that Claude Code reads as context.
- Schema errors in `plugin.json` or `.claude-plugin/marketplace.json` that could mislead the Claude Code installer.
- Issues in `.github/workflows/` — secret leakage, overly-broad permissions, or action-level code execution paths.
- Bugs in `.claude/commands/` that could trick contributors into unsafe local operations.

## Out of scope

- Bugs in Claude Code itself. Report to Anthropic.
- Bugs in `anthropics/claude-code-action`, `actions/checkout`, or other upstream GitHub Actions. Report to those projects. This repo pins them by full commit SHA (see below) to limit exposure to upstream compromise between reviews.
- Social-engineering concerns unrelated to this repo's content.

## Supply-chain practices

- **GitHub Actions pinned by SHA.** Every `uses:` reference in `.github/workflows/` is pinned to a full commit SHA with the version tag in a trailing comment. A tag can be moved to different code silently; a SHA cannot.
- **Dependabot enabled.** Weekly PRs bump the pinned SHAs, which I review and merge like any other change.
- **Branch protection on `main`.** Require PR, require 1 approval, block force-push, block deletion, require conversation resolution. Admin bypass enabled for the owner (solo-maintainer accommodation).
- **Owner-only merge.** `gh pr merge` is denied in `.claude/settings.json` for any Claude Code session in this repo — the owner clicks merge through the UI or via explicit command outside of Claude.
- **PR review workflow.** An owner-triggered `@claude` comment runs `anthropics/claude-code-action@<sha>` to review in-scope changes against `CLAUDE.md`. Advisory, not gating. Scope is restricted to `./claude/` and `./.claude/` — the human-facing `./disciplines/` tree is reviewed by humans.
