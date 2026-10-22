---
name: craft
description: "Create a new skill, or improve an existing one. Use when the user wants to make, create, or craft a skill, turn a conversation into a skill, or edit/fix an existing SKILL.md."
argument-hint: "<skill idea, or existing skill to fix>"
disable-model-invocation: true
---

# Craft

A skill is a reusable prompt for a repeatable workflow — an operating procedure, not full details. Turn an idea, or a broken skill, into one that actually works, and prove it before handing it over.

## Process

1. If this came from a conversation, use what already happened — the steps taken, the corrections made, the format wanted — as the first draft instead of starting blank.
2. Otherwise, ask what's missing: the concrete task, what should trigger it (and what shouldn't), the output shape, and any known edge cases. Offer choices where you can. Skip what the conversation already answered.
3. Editing an existing skill: read it first, and name specifically what's not working before rewriting it.
4. Write the frontmatter — a name, and a description carrying both what it does and exactly when to fire. That's the only part read before the skill runs, so be specific, not categorical.
5. Write the body as an ordered procedure. Show a fixed output format as a template, not a description of one. Cut anything explaining instead of instructing.
6. Test it: pick two or three real prompts, run the skill's own instructions to produce real output for each, show prompt and output side by side.
7. Ask what's off. Fix and rerun until it's right — generalize the fix, don't patch for the one prompt that failed.
8. Show the final SKILL.md as a copyable block. Don't write it to disk or package it unless asked.

## Boundaries

- Don't hand over a skill untested.
- Don't ask more questions than the conversation hasn't already answered.
- Don't run a full benchmarking or description-optimization pass — that's a different, heavier skill.

## Return

The finished SKILL.md, and the test prompts it was checked against.
