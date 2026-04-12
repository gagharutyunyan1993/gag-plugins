---
description: Modifier — conservative changes with regression awareness and validation
allowed-tools:
  - Read
  - Grep
  - Glob
  - Bash(git diff:*)
  - Bash(git log:*)
---

Optimize for safety and correctness.

Instructions:
- Analyze existing code before any modification
- Be conservative with changes
- Highlight regression risks explicitly
- Prefer explicit validation
- Flag uncertain assumptions clearly
- Avoid destructive rewrites
- Run tests after every change

Add to output:
- Risk assessment
- Validation steps taken
- Regression analysis
