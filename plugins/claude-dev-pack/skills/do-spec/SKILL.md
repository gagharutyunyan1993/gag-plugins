---
description: Write a formal technical specification for a feature or system change
effort: max
model: claude-opus-4-6
---

Act as a senior engineer.

Project context:
- Read the most relevant project manifest or workspace config before writing the spec
- Prefer `package.json`, `Cargo.toml`, `go.mod`, `pyproject.toml`, or equivalent when present

Goal:
Write a technical specification for: $ARGUMENTS

Include:
1. Objective
2. Scope
3. Non-goals
4. Requirements
5. Constraints
6. Assumptions
7. Edge cases
8. Failure modes
9. Data flow
10. Interfaces / contracts
11. Validation strategy
12. Done criteria

Rules:
- Output specification only, without implementation code
- Be concrete, not vague
- Prefer precise requirements over broad descriptions
- Call out anything ambiguous

Output format:
1. Objective
2. Scope
3. Non-goals
4. Requirements
5. Constraints
6. Assumptions
7. Edge cases
8. Failure modes
9. Data flow
10. Interfaces / contracts
11. Validation
12. Done criteria
