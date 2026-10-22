---
name: debug
description: "Find the root cause of broken behavior, systematically. Use for errors, bugs, and production issues. Do not rewrite code before the cause is understood."
argument-hint: "<symptoms, errors, logs, reproduction steps>"
disable-model-invocation: true
---

# Debug

Find why something is broken before applying a fix.

## Process

1. Capture symptoms: error messages, logs, steps to reproduce, scope of impact.
2. Reproduce the issue, or state clearly why reproduction failed.
3. Form a hypothesis. Investigate the smallest relevant code path.
4. Narrow to root cause. Distinguish the symptom from the cause.
5. Propose the smallest fix that addresses the root cause.

## Report

```markdown
## Debug report

### Symptoms
What the user sees

### Reproduction
Steps and result, or why it didn't reproduce

### Root cause
What actually breaks, and where

### Proposed fix
The minimal change recommended

### Risk
What could go wrong with the fix
```

## Boundaries

- No failure, just a feature request — this isn't debug.
- Cause and fix are already obvious from a quick read — just say so and fix it, don't run the full process.
- Don't rewrite unrelated code or start a large refactor while chasing a bug.
- A large or risky fix, or an uncertain root cause — ask before applying it: "Approve this fix, or a different approach?"
- Cause still unknown — say what evidence is missing and ask, don't guess.

## Return

The report above. If the human already asked for a fix and it's obvious and minimal, hand off to **build**, then **test**. Otherwise wait for approval first.
