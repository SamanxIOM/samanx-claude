---
description: Quick code scan — surface-level pass for obvious issues
---

Do a **quick** sweep of the repo using glob/grep-style searches. This should finish in **seconds**, not minutes, and should not read entire files end-to-end. Token cost should stay low.

Look for surface-level issues only:

- **Obvious red flags:** `TODO`, `FIXME`, `XXX`, `HACK` markers; leftover `console.log` / `print` / debug logging; hardcoded secrets, credentials, API keys, or passwords; hardcoded local paths (e.g. `/Users/...`).
- **Dead code:** unused imports, unreachable code after `return` / `throw`, large commented-out blocks.
- **Surface smells:** typos in code/identifiers, suspicious comparisons (`== null` vs `=== null`, assignment in conditional), obvious copy-paste errors.

Best for: "just looking around" / a sanity check before moving on.

Present the findings in a table, grouped by type (e.g. bug, security, dead code, performance, style, etc.). Include the file path and line number for each finding so the user can jump straight to it.

This is a **fly-by**. Anything that requires tracing logic across multiple files, reasoning about data flow, or auditing control flow belongs in `/scan-deep` instead — call that out explicitly if you notice something that needs a deeper look.
