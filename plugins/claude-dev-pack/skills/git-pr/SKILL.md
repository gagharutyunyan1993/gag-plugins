---
description: Generate a pull request with auto-generated description and final review
disable-model-invocation: true
allowed-tools:
  - Bash(git *)
  - Bash(gh *)
---

Act as a senior engineer.

PR context:
!`git branch --show-current`
!`git status --short`
!`git log --oneline -10`

Goal:
Create a clean pull request.

Process:
1. Analyze all commits on this branch
2. Run a final review pass on the changes
3. Write a clear PR title (under 70 characters)
4. Write a structured PR description
5. Push and create the PR

Rules:
- Title: concise, descriptive, under 70 characters
- Description uses the template below
- Flag any issues found during the final review
- Halt before push if critical issues are found — report them first
- Identify the likely base branch before drafting the PR and state the assumption if it is unclear

PR description template:
## Summary
- [key changes as bullet points]

## Test plan
- [how to verify the changes]

## Risks
- [potential issues or regression risks]
