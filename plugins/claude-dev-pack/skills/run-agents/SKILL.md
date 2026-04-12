---
description: Multi-role pipeline — Planner, Engineer, Tester, Reviewer with isolated context
effort: max
context: fork
disable-model-invocation: true
---

Use four roles in sequence with isolated context.
Spawn each role via Task() for genuine independence — each role operates without seeing prior reasoning.

1. Planner
   - defines approach
   - identifies risks
   - sets done criteria

2. Engineer
   - implements the solution
   - explains key decisions

3. Tester
   - writes tests for the implementation
   - covers edge cases and failure modes
   - validates correctness

4. Reviewer
   - critiques the result independently
   - identifies remaining issues
   - proposes final improvements

Rules:
- Keep roles isolated — use Task() subagent calls per role
- Tester must cover happy path and edge cases
- Reviewer must challenge, not approve
- Final output must merge the best result after review

Output format:
1. Planner output
2. Engineer output
3. Tester output
4. Reviewer output
5. Final merged result
