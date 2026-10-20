---
name: design
description: "Decide what to build and how before coding. Use for features, interfaces, data, security, or non-trivial changes. Writes docs/<feature>/design.md and waits for approval."
argument-hint: "<feature, problem, or PROJECT.md context>"
---

# Design

Settle important product and technical choices before implementation.

## Process

1. Read the request, `PROJECT.md`, project `AGENTS.md`, relevant code, and prior **understand** output.
2. Identify decisions implementation must not invent silently.
3. Interview the user in rounds until the design has no open branches. Map decisions as a tree: each decision may depend on others.
   - The **frontier** is every decision whose prerequisites are already settled. Ask the whole frontier in one round.
   - Number each question. Give a recommended answer for each, and word it so "yes" accepts that recommendation.
   - Wait for answers. Settled decisions open new questions, so recompute the frontier and ask the next round. A question that depends on an unanswered one waits for a later round.
   - Find facts yourself. Read the code, `PROJECT.md`, and `docs/flows/` with read-only tools before asking. Ask the user only for decisions.
   - Stop when the frontier is empty. Put every settled choice in **Decisions**, and every unsettled one in **Open questions**.
4. Write the design — `docs/<feature-slug>/design.md` by default, chat-only for a small change if the user prefers.
5. Tailor sections to the task. Include only what matters.
6. Stop and ask: "Please review the design. Reply approved or request changes."

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

## Credit

The interview method in step 3 is adapted from Matt Pocock's `grilling` skill (MIT License, Copyright (c) 2026 Matt Pocock), in [mattpocock/skills](https://github.com/mattpocock/skills).

## Return

The design, ready for review. Once approved: several steps or sessions go to **plan**; one clear implementation pass goes to **build**.
