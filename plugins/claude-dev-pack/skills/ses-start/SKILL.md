---
description: Load context from previous session notes and establish working state
effort: low
---

Start a new work session.

Process:
1. Read `.claude/session-notes.md` if it exists
2. Read recent git history if the workspace is a git repository
3. Summarize what was done previously and what's pending
4. Confirm the current working context with the user

Rules:
- If `.claude/session-notes.md` does not exist, continue without it
- If the workspace is not a git repository, infer the current state from the file tree and recent edits

Output:
- Previous session summary (if notes exist)
- Current project state
- Suggested next steps
