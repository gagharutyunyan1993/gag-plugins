---
description: Generate tests by reading existing test patterns first
effort: high
---

Act as a senior engineer.

Existing test patterns:
- Read representative existing test files before writing new tests
- Prefer files near the feature area and the project's primary test directories

Goal:
Write tests for: $ARGUMENTS

Process:
1. Read existing test files to understand the project's testing style
2. Match the existing assertion framework and patterns
3. Write tests covering:
   - Happy path
   - Edge cases
   - Error conditions
   - Boundary values
4. Run the tests to verify they pass

Rules:
- Follow the project's existing test conventions
- Use the same testing framework already in use
- Test behavior, not implementation
- Each test should test one thing
- Use descriptive test names

Output format:
1. Test file(s) created
2. Test run results
3. Coverage summary
