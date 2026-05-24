---
description: Deploy this repo's global Claude config to the local machine.
---

This skill copies the contents of `for-claude-global/` in this repo to the user's `~/.claude/` directory so that every Claude Code session on this machine picks up the shared config.

## Determine the Claude config directory

Detect the current OS and use the correct path. All references to `~/.claude/` below mean the resolved config directory for the current platform.

- **macOS / Linux:** `~/.claude/`
- **Windows:** `%USERPROFILE%\.claude\`

## Sync skills

1. If `~/.claude/skills/` does not exist, create it.
2. Copy the entire contents of this repo's `for-claude-global/skills/` into `~/.claude/skills/`, preserving the subfolder structure. Overwrite any existing files with the same name, but leave other skills that exist locally untouched.

## Sync CLAUDE.md

Copy this repo's `for-claude-global/CLAUDE.md` to `~/.claude/CLAUDE.md`, overwriting any existing file at that path.

## Verify

After copying, list the contents of `~/.claude/skills/` and confirm `~/.claude/CLAUDE.md` exists. Report what was deployed.