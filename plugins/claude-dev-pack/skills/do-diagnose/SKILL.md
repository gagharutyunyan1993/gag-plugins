---
description: Investigate an unclear bug systematically with hypothesis-driven loop
effort: high
---

Act as a senior engineer.

Goal:
Investigate an unclear bug or failure systematically.

Loop:
1. Define the observed failure
2. Compare expected vs actual behavior
3. Form hypotheses
4. Identify the highest-probability cause
5. Propose or apply a test
6. Update the hypothesis
7. Repeat until root cause is isolated

Rules:
- Focus on evidence, not guesswork
- Prefer the smallest test that increases confidence
- Separate confirmed findings from hypotheses
- If the bug cannot be reproduced, say so explicitly
- Write hypotheses and findings to `.claude/debug.log` for diagnostic trail across sessions

Output format:
1. Observed issue
2. Expected vs actual
3. Hypotheses (ranked by probability)
4. Most likely cause
5. Test / investigation step
6. Findings
7. Next fix or next step

Done when:
- Root cause is isolated, or
- The remaining uncertainty is clearly bounded
