---
name: design
description: "Decide what to build and how before coding. Use for features, interfaces, data, security, or non-trivial changes. Writes docs/<feature>/design.md and waits for approval."
argument-hint: "<feature, problem, or PROJECT.md context>"
disable-model-invocation: true
---

# Design

Interview the user relentlessly until the design is settled, then write it down and wait for approval.

## Process

1. Read the request, `PROJECT.md`, project `AGENTS.md`, relevant code, and prior **understand** output.
2. Run the **Interview method** below until the frontier is empty.
3. Write the design — `docs/<feature-slug>/design.md` by default, chat-only for a small change if the user prefers. Put every settled choice in **Decisions**, and every unsettled one in **Open questions**.
4. Tailor sections to the task. Include only what matters.
5. Stop and ask: "Please review the design. Reply approved or request changes."

## Interview method

Interview the user relentlessly until you reach a shared understanding. Map this as a **design tree**: every decision branches into the decisions that hang off it.

Work the tree in **rounds**. The **frontier** is every decision whose prerequisites are already settled: the questions you can ask _now_ without guessing at answers you haven't heard yet. Ask the whole frontier in one round: number each question and give your recommended answer. Then wait for the user's answers before the next round.

Format a round like so:

```
❓ **Q1** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

➡️ <your recommended answer>

---

❓ **Q2** - **<question title>**: <question body, might be multiple paragraphs, including multiple choices>

➡️ <your recommended answer>
```

Word each question so "yes" accepts your recommended answer.

Each round the user answers reshapes the tree: settled decisions push the frontier outward and unblock questions that depended on them. Recompute the frontier and ask the next round. A question whose answer depends on another question still open in this round belongs to a _later_ round, not this one.

Finding _facts_ is your job, never the user's. When a frontier question needs a fact from the environment (filesystem, tools, etc.), dispatch a sub-agent to find it; don't ask the user for anything you could look up yourself. Don't block on it: a running exploration is an unsettled prerequisite, so only the questions downstream of it wait for the sub-agent to report; ask the rest of the frontier now. The _decisions_ are the user's: put each to them and wait.

The session is done when the frontier is empty: every branch of the design tree visited, nothing left silently assumed. Do not act on it until the user confirms you have reached a shared understanding.

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

The interview method above is taken from Matt Pocock's `grilling` skill (MIT License, Copyright (c) 2026 Matt Pocock), in [mattpocock/skills](https://github.com/mattpocock/skills).

## Return

The design, ready for review. Once approved: several steps or sessions go to **plan**; one clear implementation pass goes to **build**.
