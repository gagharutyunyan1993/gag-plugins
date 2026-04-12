---
description: Fix a bug using OODA loop — root cause analysis with minimal change
effort: high
---

Act as a senior engineer.

Recent changes context:
!`git diff HEAD`

Goal:
Fix the bug: $ARGUMENTS
Address the root cause with the smallest justified change.

Use this method:
1. Observe — describe the failure briefly
2. Orient — identify the likely root cause
3. Decide — choose the minimal correct fix
4. Act — implement the fix
5. Verify — run tests to confirm the issue is resolved without breaking expected behavior

Rules:
- Fix root cause, not symptoms
- Prefer minimal changes
- Preserve existing logic
- Keep changes limited to the affected code path
- If root cause is uncertain, say so explicitly

Output format:
1. Symptom
2. Root cause
3. Fix
4. Test verification
5. Regression risks

Done when:
- The failure is addressed at the root cause level
- The fix is as small as reasonably possible
- Tests pass after the fix
