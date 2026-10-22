---
name: improve
description: "Simplify existing code without changing intended behavior. Use when code works but is hard to maintain."
argument-hint: "<files, module, or area to improve>"
disable-model-invocation: true
---

# Improve

Make code clearer and easier to maintain without changing intended behavior.

## Process

1. Read the target code and understand its current behavior.
2. State what will not change — public behavior, interfaces, outputs.
3. Refactor in small steps. Prefer local clarity over large moves.
4. Run tests or other checks to prove behavior is preserved.

## Boundaries

- A bug needs fixing — use **debug** then **build**, not this.
- A new feature is wanted — use **design** and **build**, not this.
- No tests or other way to verify behavior is preserved — don't refactor blind.
- Don't mix a behavior change into cleanup.
- Refactor scope growing beyond the stated target, or touching a public interface — ask before continuing.
- Behavior needs to change after all — stop, switch to **design** and **build**.

## Return

Refactored code, a summary of what improved, and evidence that behavior is preserved. Hand off to **test** to confirm and report.
