---
name: model-check
description: "Suggest the model and effort level that fit a task, then wait for confirmation before starting. Use at the start of every new task and every new phase (for example, design approved → build), even small ones. Skip it for follow-ups on the task already in progress."
---

# Model check

Before starting a new task, suggest the model and effort that fit it. Then wait.

## Process

1. Pick the tier that fits the task:

   | Task | Model | Effort |
   | --- | --- | --- |
   | Quick and clear: rename, one-line fix, short reply, simple lookup | Fast | low |
   | Normal and clearly described: a feature, a draft, a summary | Strongest | medium |
   | Unclear or messy: unexplained bug, multi-file refactor, unfamiliar code, research across many pages | Strongest | high |
   | Big or hard to undo: architecture, a career or money decision, anything acted on for months | Strongest | xhigh |

2. Name the real models the current tool offers. In Claude, for example, Fast is Sonnet 5 and Strongest is Opus 5.5.
3. If the tool has no effort setting, suggest only the model.
4. If the same thing went wrong twice in this task, suggest one effort level higher. Above xhigh, that means max.
5. Print the suggestion in the format below, then stop. Don't start the task until the user confirms, even for quick tasks.

## Report

```
Suggested: Opus 5.5, high (unclear bug across 3 files)
Continue?
```

## Boundaries

- Each new phase counts as a new task. Run the check again when moving from design to plan, plan to build, and so on.
- A follow-up on the task already in progress doesn't need a new check.
- Don't start a task at max effort. Suggest max only when a task at xhigh went wrong twice.

## Return

The suggestion line. Once the user confirms, start the task with the skill it needs.
