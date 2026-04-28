# SnipVault - Agent Brief

This file is read by every coding agent (Claude Code, GitHub Copilot, others) before doing any work.
Keep it short and current.

## What this is

SnipVault is a tiny code-snippet manager: a FastAPI backend with SQLite persistence, a Click-based CLI client, and a pytest suite. Used as a teaching project for multi-agent orchestration patterns.

## Layout

```
snipvault/
├── api/              # FastAPI service, models, routes, schemas
├── cli/              # `snip` CLI - Click commands
├── tests/            # pytest suite (uses in-memory SQLite)
├── Dockerfile
├── Makefile          # `make run`, `make test`, `make lint`
├── .github/
│   ├── workflows/    # CI
│   └── copilot-instructions.md
├── .claude/
│   └── agents/       # custom Claude Code subagents
├── AGENTS.md         # this file
└── CLAUDE.md         # Claude Code-specific overrides
```

## Conventions

- **Python 3.11+**, type hints required on all public functions.
- **async-first** for I/O (`httpx.AsyncClient`, `aiosqlite`).
- **Tests:** pytest + anyio + httpx async client. Cover happy path + at least one edge case per route.
- **Lint/format:** ruff + black, enforced in CI. Don't fight the linter.
- **Errors are user-facing.** CLI error messages must be actionable (tell the user what to do).
- **No new top-level dependencies** without justification in the PR description.

## Do not touch

- `main` branch directly - always work on a feature branch and open a PR.
- `.github/workflows/` unless the task is explicitly about CI.
- Files outside your assigned scope - if you think you need to, stop and ask.

## How to work

1. Read this file, then `CLAUDE.md` (if you're Claude Code) or `.github/copilot-instructions.md` (if you're Copilot).
2. If unclear about scope, ask before writing code.
3. Open a draft PR with a checklist mapping to the task's acceptance criteria.
4. Run `make test` and include the result in the PR description.
5. Stay in your lane.
