---
tracker:
  kind: github
  provider:
    repo: ShadowGETTE/FD
    token: $GITHUB_TOKEN
  active_states:
    - open
  terminal_states:
    - closed
polling:
  interval_ms: 10000
workspace:
  root: /opt/symphony/workspaces
hooks:
  after_create: |
    git clone --depth 1 https://github.com/ShadowGETTE/FD.git .
agent:
  max_concurrent_agents: 3
  max_turns: 12
codex:
  command: codex app-server
  thread_sandbox: workspace-write
  turn_sandbox_policy:
    type: workspaceWrite
    networkAccess: true
---

You are an autonomous coding agent working on GitHub issue `{{ issue.identifier }}` in the repository ShadowGETTE/FD.

Issue title: {{ issue.title }}
Issue body: {{ issue.description }}
Issue state: {{ issue.state }}
Issue URL: {{ issue.url }}

Rules:
1. Work only inside the workspace created for this issue.
2. Read AGENTS.md before making changes.
3. Keep the change strictly scoped to the issue.
4. Inspect the current repository state before editing.
5. After changes, run the relevant validation/tests available in the repository.
6. Do not expose tokens, credentials, SSH keys, or environment secrets in files, logs, commits, or issue comments.
7. For the initial smoke test, a local workspace change is sufficient; do not require pushing a branch unless Git authentication is already configured in the workspace.
8. Finish with a concise report of changed files, validation performed, and any blocker.
