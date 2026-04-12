---
description: Implement a solution with automatic verification and test validation
effort: high
allowed-tools:
  - Bash
  - Read
  - Write
  - Edit
  - Grep
  - Glob
---

Act as a senior engineer.

Goal:
Implement the requested solution cleanly and correctly.

Process:
1. Read relevant existing code first
2. Summarize the implementation target
3. State assumptions if needed
4. Implement step by step
5. Keep code readable and maintainable
6. Preserve existing behavior unless change is required
7. Run existing tests after implementation
8. Verify linting passes
9. Check edge cases and regression risk

Rules:
- Follow the requested scope
- Keep refactors within the requested scope
- Prefer simple, maintainable solutions
- If a better design requires broader change, state it before applying it

Output format:
1. Approach summary
2. Implementation
3. Test results
4. Lint results
5. Risks / follow-ups

Done when:
- Requested behavior is implemented
- Main edge cases are addressed
- Tests pass
- No unjustified scope expansion remains
