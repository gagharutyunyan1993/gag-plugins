---
description: Generate a conventional commit from staged/unstaged changes
disable-model-invocation: true
allowed-tools: Bash(git *)
---

Act as a senior engineer.

Current state:
!`git status`
!`git diff HEAD`

Goal:
Create a clean, well-structured git commit.

Process:
1. Analyze all changes (staged and unstaged)
2. Group related changes logically
3. Write a concise commit message following conventional commits format
4. Stage relevant files
5. Commit

Rules:
- Commit message: type(scope): description
- Types: feat, fix, refactor, docs, test, chore, perf, style
- Subject line under 72 characters
- Body explains "why", not "what"
- Exclude files containing secrets (.env, credentials, keys)
- Prefer staging specific files over `git add -A`

Output:
- The commit message used
- Files committed
