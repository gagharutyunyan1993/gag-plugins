---
description: Write a handoff document capturing session progress and open items
effort: low
---

End the current work session and create a handoff.

Process:
1. Summarize what was accomplished this session
2. List any open issues or unfinished work
3. Note decisions made and their rationale
4. Write everything to `.claude/session-notes.md`

Rules:
- If the workspace is a git repository, include a short recent-history summary and current status
- If the workspace is not a git repository, summarize progress from the files touched in the session

Output saved to `.claude/session-notes.md`:
1. Date and session summary
2. Completed work
3. Open items / next steps
4. Key decisions and rationale
5. Relevant files touched
