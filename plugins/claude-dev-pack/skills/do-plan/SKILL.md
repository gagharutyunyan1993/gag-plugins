---
description: Create a structured implementation plan before writing code
effort: high
---

Act as a senior engineer.

Current project state:
!`git log --oneline -10`
!`git diff --stat`

Project inspection:
- Inspect representative source files in the relevant area before planning
- Prefer files closest to the requested feature, bug, or subsystem

Goal:
Create a clear implementation plan for: $ARGUMENTS

Instructions:
1. Restate the problem briefly
2. Identify assumptions and missing context
3. Read relevant existing code before planning
4. Break the work into ordered steps
5. Call out edge cases and risks
6. Define the implementation approach
7. Define what "done" means

Rules:
- Output plan only, without code
- Prefer a practical step-by-step plan
- Be explicit about trade-offs
- If context is incomplete, proceed with reasonable assumptions and state them

Output format:
1. Problem summary
2. Assumptions
3. Plan
4. Edge cases / risks
5. Done criteria

Stop after the plan.

Optional: save plan to `plans/YYYYMMDD-<feature>.md` for searchable archive.
