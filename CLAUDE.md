# Claude Code Instructions for SnipVault

> Read `AGENTS.md` first. This file is the Claude-Code-specific overlay.

## Orchestration defaults

- For **independent work** across the three components (api/cli/tests), spawn parallel subagents using the `Agent` tool with `isolation: "worktree"` and one branch per subagent (`feat/<area>`).
- For **coordinated features** (e.g. anything touching api + cli), use **Plan &rarr; Explore &rarr; general-purpose &rarr; security-reviewer** in sequence.
- Open a **draft PR per branch** with `gh pr create --draft`. Don't auto-merge; the human merges after review.

## Subagents available

- **Plan** (built-in) - design first, no code.
- **Explore** (built-in) - read-only mapping of the codebase.
- **general-purpose** (built-in) - implementation.
- **security-reviewer** (custom, `.claude/agents/security-reviewer.md`) - run on the diff before merge.

## Token discipline

- Use **Haiku** for exploration and search-heavy subagents.
- Use **Sonnet** for steady implementation work.
- Use **Opus** only for hard reasoning (architecture, complex merges, deep debugging).
- Run `/cost` before any "shall I keep going?" decision.

## What requires a human checkpoint

- Any change to `.github/workflows/` (CI) - approve the plan first.
- Any database schema change - approve the migration plan first.
- Any deletion of files - confirm before doing it.
- Any merge to `main` - never auto-merge.

## What does NOT require a human checkpoint

- Edits inside an assigned scope (api/, cli/, tests/) on a feature branch.
- Running tests, lints, formatters.
- Opening draft PRs.
