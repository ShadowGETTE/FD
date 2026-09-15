# Agent rules

This repository is the pilot target for Symphony/Codex orchestration.

## General
- One GitHub issue = one isolated Symphony workspace.
- Do not make unrelated refactors.
- Never commit secrets, tokens, credentials, private keys, or machine-specific files.
- Prefer the smallest correct change.
- Inspect before editing; validate after editing.

## Roles
Symphony may dispatch multiple concurrent Codex workers. Treat the issue scope as the role boundary:
- backend: application logic, API, tests
- frontend: UI/client changes
- devops: deployment, systemd, Docker, CI/CD
- reviewer: inspect diffs, tests, security, regressions; avoid feature expansion

## Completion report
Every worker should finish with:
1. files changed;
2. validation/tests executed;
3. remaining risks or blockers.
