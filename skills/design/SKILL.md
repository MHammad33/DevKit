---
name: design
description: "Decide what to build and how before coding. Use for features, interfaces, data, security, or non-trivial changes. Writes docs/<feature>/design.md and waits for approval."
argument-hint: "<feature, problem, or PROJECT.md context>"
disable-model-invocation: true
---

# Design

Write up the settled decisions from the `grill-me` conversation, then wait for approval. Design does not interview.

## Process

1. Check the conversation for a `grill-me` session on this task. If there is none, say "Run `/grill-me` first." and stop. Do not ask your own questions.
2. Read the request, `PROJECT.md`, project `AGENTS.md`, relevant code, and prior **understand** output.
3. Write the design from the grilling — `docs/<feature-slug>/design.md` by default, chat-only for a small change if the user prefers. Put every settled choice in **Decisions**, and every unsettled one in **Open questions**.
4. Tailor sections to the task. Include only what matters.
5. Stop and ask: "Please review the design. Reply approved or request changes."

## Design document sections

Use these headings. Omit what doesn't apply.

```markdown
# <Title>

> Status: Proposed — awaiting approval

## Summary
What changes, for whom, and the main tradeoff.

## Context
Current behavior and why it's insufficient.

## Proposed approach
How it works end to end.

## Decisions
What you chose, what you rejected, and why.

## Requirements
Testable behavior and constraints.

## Invariants
Rules that must not break (when relevant).

## Error behavior
Important failure paths (when relevant).

## Test strategy
How to verify acceptance criteria.

## Out of scope
What this design doesn't include.

## Open questions
Unresolved items, and whether they block implementation.
```

## Boundaries

- An obvious bug with a clear fix, a rename, a typo, a config tweak — skip design.
- Constraints and v1 scope are already fully settled in `PROJECT.md` — skip design.
- Don't run **plan** or **build** until the human approves or asks for changes.

## Return

The design, ready for review. Once approved: several steps or sessions go to **plan**; one clear implementation pass goes to **build**.
