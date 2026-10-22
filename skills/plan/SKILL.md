---
name: plan
description: "Split approved design into tasks by working result, one build pass each. Use when work spans multiple build sessions. Skip for single-pass work (use build) or unapproved design (use design). Does not write code."
argument-hint: "<approved design path or feature name>"
disable-model-invocation: true
---

# Plan

Turn approved design into tasks a fresh **build** agent can execute using only what design already decided. Split by working result, not by file or layer.

## Process

1. Start from the approved design and the code it affects. Read `PROJECT.md` for product scope and `AGENTS.md` for commands and conventions, when the repo has them. Missing them, use the design plus what the human told you, and call out anything still unverifiable before listing tasks.
2. If a choice would change what the product does, how parts connect, what data crosses a boundary, or how you'd verify the work — stop, and tell the human to resolve it in **design**. Don't bury an open question inside a task.
3. Slice by what works, not where it lives. Each task finishes in one **build** pass and leaves something that actually runs or behaves correctly — not a layer, folder, or file group.
4. When two tasks would need the same answer, combine that work or put it in the earlier task. If cleanup would disguise a behavior change, give it its own task.
5. Put tasks in dependency order. Label a milestone only where there's a real checkpoint — something to demo, review, or hand off.
6. Post the ordered task list in chat.

## Plan shape

```markdown
## Plan: <feature>

### Task 1: <title>
Goal:
Files likely touched:
Done when:
Depends on: none

### Task 2: <title>
...
```

## Boundaries

- Nothing approved yet — that's **design**, not this.
- One build session is enough — go straight to **build**, skip this.
- Don't write a plan file unless the human wants one.
- Don't build, test, or edit code. The job ends at the list.

## Return

The ordered task list above. For a large plan, ask first if the order or scope looks wrong. Then: "Start with Task 1: Use the build skill. <task summary>"
