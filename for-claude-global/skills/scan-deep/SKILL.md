---
description: Deep code audit — thorough cross-file review
---

Do a **thorough** audit of the repo. This will take **minutes** (not seconds) and burn significantly more tokens than `/scan-quick` — that cost is expected and accepted by the user when they invoke this command.

Read files end-to-end. Trace data flow across modules. Reason about control flow, not just syntax.

Check for:

- **Logic bugs:** missing null/undefined checks, off-by-one errors, incorrect boundary conditions, wrong operator precedence, mishandled empty collections.
- **Concurrency:** race conditions, missing locks, unsafe shared mutable state, async functions whose results are never awaited.
- **Error handling:** silently swallowed errors, missing error paths, exceptions that leak sensitive info, retry loops with no backoff.
- **Security:** broken authentication or permission flows, injection risks (SQL, command, XSS), unsafe deserialisation, exposed secrets, insecure defaults, vulnerable or outdated dependencies.
- **Cross-file consistency:** API contract mismatches between caller and callee, divergent assumptions about shared data structures, dead exports, types/interfaces that have drifted out of sync with their implementations.

Best for: "I'm about to ship — go over it properly."

Present the findings in a table, grouped by type (e.g. bug, security, dead code, performance, style, etc.). For each finding, include:

- **File path + line number** so the user can jump straight to it.
- **A brief description** of what's wrong.
- **A suggested fix** (or, if uncertain, the question the user needs to answer to decide on a fix).

Be willing to flag things you're not 100% sure about — say so explicitly ("possible race condition — depends on whether `foo` is ever called from a worker thread"). Surface-level issues that `/scan-quick` would catch are in scope here too, but de-prioritise them.
