---
name: build
description: "Implement the smallest complete change using test-driven development (red, green, refactor). Use when scope is clear, design is approved, or the task is a small decided fix."
argument-hint: "<task, plan item, or approved design path>"
---

# Build

Implement the requested change with minimal scope, one test-driven cycle at a time.

## Process

1. Read the task, the approved design or plan, `PROJECT.md`, and project `AGENTS.md`.
2. State what you're about to change, in one short paragraph.
3. Break the change into behaviors the acceptance criteria describe. Pick the smallest one to start.
4. Red: write a test for that behavior. Follow existing test patterns. Run it and confirm it fails for the expected reason. If it passes already, the test is wrong or the behavior exists; stop and check.
5. Green: write the smallest code that makes the test pass. Follow existing project patterns. No extra features.
6. Refactor: clean up the code you just wrote, with the test still green. Don't touch unrelated code.
7. Repeat steps 3 to 6 for the next behavior until the change matches scope.
8. Stop once implementation matches scope.

Run only the tests for the behavior you're working on. The full suite belongs to **test**.

## Boundaries

- Root cause unknown — use **debug** first, not this.
- Important choices still open — use **design** first, not this.
- Behavior-preserving cleanup with no feature — use **improve** instead.
- Don't refactor unrelated code.
- Don't expand scope, or make an architectural choice not already approved, without asking first.
- Don't run full verification here — that's **test**.
- Don't write production code before its failing test, unless the project has no test setup. If it has none, say so and ask before adding one.
- Don't skip the red step to save time.

## Return

Code changes and their tests, and a short summary of what changed and why. List each behavior you covered and the test that covers it. Hand off to **test**: "Use the test skill. Verify the build changes against the acceptance criteria."
