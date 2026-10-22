---
name: review
description: "Independent read-only review of an implementation. Reports findings and a verdict without editing code. Use for non-trivial or security-sensitive changes, or when the user asks for a review."
argument-hint: "<branch, PR, diff, or change description>"
disable-model-invocation: true
context: fork
---

# Review

Critically evaluate an implementation without changing it.

## Process

1. Read `$ARGUMENTS` — the branch, PR, diff, or change description — plus any design doc and project `AGENTS.md`.
2. Check correctness against stated requirements, regressions, security (auth, input validation, secrets, trust boundaries), simplicity, and proof — were tests run, what's still unverified.
3. Report findings with a severity and a verdict.

## Report

```markdown
## Review

### Findings
- [Must fix | Should fix | Could fix] description

### Verdict
APPROVE | FIX REQUIRED | NEEDS DISCUSSION

### Notes
What the author should do next
```

## Boundaries

- A typo or one-line obvious fix — skip review.
- Nothing's been implemented yet — there's nothing to review.
- The user wants the code fixed, not reviewed — that's **build**.
- Don't edit the code. Findings only.

## Return

The report above. FIX REQUIRED goes to **build**, then **test**, then review again if needed. APPROVE means done, or merge per the project's process. NEEDS DISCUSSION means the human decides before more code.
