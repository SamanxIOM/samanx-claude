---
description: Prepare a fresh repo with docs branch, gitignore baseline, and PR template.
---

- If the user is on the main branch or master branch, create a branch. Follow standard GitHub conventions (e.g. `feat/…`, `fix/…`, `chore/…`, `docs/…`).

- If a `.gitignore` file does not already exist at the repo root, create one. 

- For each individual line below, check whether that exact line is already present in `.gitignore`. Append any missing lines; do not duplicate lines that are already there.

  ````
  # VS Code files for those working on multiple tools
  .vscode/*
  !.vscode/settings.json
  !.vscode/tasks.json
  !.vscode/launch.json
  !.vscode/extensions.json
  !.vscode/*.code-snippets

  # macOS
  .DS_Store

  # Claude Code
  settings.local.json

  # Environment
  .env
  ````

- Create a folder called `docs` at the repo root.

- In `docs/`, create a file called `pull_request_template.md` with exactly the following contents:

  ````markdown
  # Summary of Change
  Summary of change
  ````
