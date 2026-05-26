---
name: claude-global-update
description: Deploy the "for-claude-global" config to global Claude
---

This skill copies the contents of `for-claude-global/` in this repo to the user's `~/.claude/` directory so that every Claude Code session on this machine picks up the shared config.

## Determine the Claude config directory

Detect the current OS and use the correct path. All references to `~/.claude/` below mean the resolved config directory for the current platform.

- **macOS / Linux:** `~/.claude/`
- **Windows:** `%USERPROFILE%\.claude\`

## Sync skills

1. If `~/.claude/skills/` does not exist, create it.
2. Copy the entire contents of this repo's `for-claude-global/skills/` into `~/.claude/skills/`, preserving the subfolder structure. Overwrite any existing files with the same name, but leave other skills that exist locally untouched.

## Sync settings.json

Deep-merge this repo's `for-claude-global/settings.json` into the existing `~/.claude/settings.json`:

1. Read the existing `~/.claude/settings.json` (if it doesn't exist, treat it as `{}`).
2. Read this repo's `for-claude-global/settings.json`.
3. Deep-merge the two objects:
   - For object values: recursively merge (repo values win on key conflicts).
   - For array values (e.g. `permissions.allow`): concatenate both arrays and deduplicate.
4. Write the merged result to `~/.claude/settings.json`.

## Sync CLAUDE.md

Merge this repo's `for-claude-global/CLAUDE.md` into `~/.claude/CLAUDE.md` using a managed-block delimiter so hand-edited content in the global file is preserved.

1. Read the existing `~/.claude/CLAUDE.md` (if it doesn't exist, treat it as empty).
2. Read this repo's `for-claude-global/CLAUDE.md`.
3. Wrap the repo content in delimiters:
   ```
   <!-- BEGIN managed by sam-claude-config -->
   {repo CLAUDE.md content}
   <!-- END managed by sam-claude-config -->
   ```
4. If the existing file already contains the `BEGIN`/`END` delimiters, replace everything between them (inclusive) with the new wrapped block.
5. If the existing file does not contain the delimiters, append the wrapped block to the end of the file.
6. Write the result to `~/.claude/CLAUDE.md`.

## Verify

After copying, list the contents of `~/.claude/skills/` and confirm `~/.claude/CLAUDE.md` and `~/.claude/settings.json` exist. Report what was deployed.

On Windows, use the PowerShell tool for directory listing — the Bash tool mangles backslashes in Windows paths. On macOS/Linux, use the Bash tool.