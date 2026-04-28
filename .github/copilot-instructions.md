# GitHub Copilot Instructions for SnipVault

> Read `AGENTS.md` first. This file is the Copilot-specific overlay.

## What you'll be asked to do

You'll typically be assigned issues by a human via the GitHub UI (`@copilot` assignee) or invoked from VS Code in Agent Mode. Stay tightly scoped to the issue or chat task.

## Conventions (recap)

- Python 3.11+, type hints required on changed code.
- async-first for I/O.
- Tests use pytest + anyio + httpx async client.
- ruff + black for lint/format - don't fight the linter.

## Working on an assigned issue

1. Read `AGENTS.md` and this file.
2. Read the issue body fully - especially **acceptance criteria** and **constraints**.
3. Open a **draft PR** with a checklist mirroring the acceptance criteria.
4. Stay strictly within the directories named in the issue's scope.
5. Run `make test` and `make lint` before pushing. Include results in the PR body.
6. Do not refactor unrelated code, even if you see something you'd improve - file a separate issue.

## Working in VS Code Agent Mode

- Stay focused on the user's current task. If they ask for a function, write that function plus its tests, not a full refactor.
- When you run a tool (terminal command, file write, test), narrate what you're doing.
- If you hit ambiguity, ask a clarifying question in chat instead of guessing.

## What to flag in PR descriptions

- Any new third-party dependency.
- Any change to public API shape (route signatures, CLI flags, response schemas).
- Anything that requires a database migration.
- Anything you weren't sure about - call it out so the reviewer can focus.

## What NOT to do

- Don't touch `.github/workflows/` unless the issue is explicitly about CI.
- Don't merge your own PR.
- Don't auto-resolve review comments without addressing them.
