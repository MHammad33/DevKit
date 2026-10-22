---
name: ask-hammad
description: "Pick the right path for a task. Asks a few questions, names the size (small, medium, large, hotfix) and prints the skills to run in order. Read-only."
argument-hint: "<task you want to start>"
disable-model-invocation: true
---

# Ask Hammad

Route the task to a path. Do not start the work.

## Process

1. Read the task from the arguments. If there are none, ask for it in one line.
2. Ask up to three short questions, only for what the task does not already answer:
   - Is something broken in production?
   - Is it a bug, a tweak, or a clear task? Or a new feature?
   - Will it fit in one session?
3. Name the size and print the path.
4. Stop. Do not run any skill.

## Paths

| Size | Fits | Path |
| --- | --- | --- |
| Small | Bug, tweak, clear task | `build` → `test`. Run `debug` first for a bug. |
| Medium | One feature, one session | `grill-me` → `build` → `test` → `review` |
| Large | Multi-session feature, new project | `grill-me` → `design` → approve → `plan` → `build` → `test` → `review` |
| Hotfix | Production is failing | `debug` → approve the fix → `build` (regression test first) → `test` → `review` |

## Stage names

Users may say a stage instead of a skill. Map it here.

| Stage | Skill |
| --- | --- |
| Define | `grill-me` |
| Design | `design` |
| Plan | `plan` |
| Build | `build` |
| Verify | `test` (`debug` when it fails) |
| Review | `review` |
| Ship | none yet |

## Helpers

- Unfamiliar code: add `understand` before the path.
- Working code that is hard to maintain: use `improve`, then `test`.

## Return

- The size, and one line on why.
- The path, with real skill names.
- For large: "Run `design` in the same session as `grill-me`. It writes up that conversation."
- The first command to run, for example `/grill-me <task>`.
