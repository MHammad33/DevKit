---
name: test
description: "Verify a change with evidence. Use after build or improve, or when the user asks to verify a branch, fix, or feature."
argument-hint: "<change description, acceptance criteria, or design path>"
disable-model-invocation: true
---

# Test

Prove whether the change works. Report evidence, not assumptions.

## Process

1. Read the change, acceptance criteria, design test strategy, and project `AGENTS.md` commands.
2. List what must be verified.
3. Run relevant automated tests, lint, and type checks with project commands.
4. Check affected failure paths where they matter.
5. For UI behavior, verify in a real browser when the project has one and automated tests don't cover it.
6. Report each criterion as pass, fail, or unverified, with a reason.

## Report

```markdown
## Test report

### Criteria
- [PASS|FAIL|UNVERIFIED] AC-1: ...

### Commands run
- `npm test` — result

### Unverified
- What could not be checked, and why
```

## Boundaries

- No code changed yet — this isn't for reviewing a design or plan. Wait until build produces something.
- Don't leave an unverified criterion without a reason.

## Return

The report above, with every criterion settled as pass, fail, or explicitly unverified. Failures go back to **build**, then test again. A non-trivial or risky change that passes goes to **review**. A trivial fix that passes is done.
