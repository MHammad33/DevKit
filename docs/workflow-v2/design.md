# Workflow v2: fewer skills, user-invoked, four paths

> Status: Approved

## Summary

Remove `write-a-prd` and add `ask-hammad`, so the set stays at 14 skills with fewer overlaps. Make every skill manual-only except `idea`, which stays untouched. Add four work paths (small, medium, large, hotfix) and a router skill, `ask-hammad`, so nothing runs that you didn't call. Use Matt Pocock's mechanics and Addy Osmani's stage names.

## Context

- Several skills overlap: `idea`, `grill-me`, `design` and `write-a-prd` all do "talk until clear". `design` and `write-a-prd` both write a spec, in two different places.
- The process feels heavy for small work. Every skill is model-invocable, which costs tokens and can start work you didn't ask for.
- You work on side projects and at a job. The tracker at work is Basecamp today and may change.

## Proposed approach

### Principles

1. **User-invoked only.** Every skill sets `disable-model-invocation: true`.
2. **Argument hints.** Every skill has an `argument-hint`.
3. **Grill first** for anything bigger than a small task.
4. **Repo files are the default home** for specs and task lists: `docs/<feature>/`.
5. **The tracker is a last step.** No skill names a tracker. A project's `AGENTS.md` carries one line, for example `Tracker: Basecamp, publish by hand`. Changing trackers means editing that line.

### Stages

Seven stages. They follow Osmani's names, with his "define" split into define and design:

| Stage | Question | Skill |
| --- | --- | --- |
| 1. Define | What problem, and for whom? | `grill-me` |
| 2. Design | How will we solve it? | `design` |
| 3. Plan | In what order? | `plan` |
| 4. Build | Make it, test-first. | `build` |
| 5. Verify | Does it work? | `test` (`debug` when it doesn't) |
| 6. Review | Is it good enough to merge? | `review` |
| 7. Ship | Get it out. | later |

`understand` and `improve` are helpers outside the flow. Call `understand` before any path in unfamiliar code. Call `improve` on working code that is hard to maintain.

### Four paths

Each path skips stages.

| Size | Example | Path |
| --- | --- | --- |
| Small | Bug, tweak, clear task | `build`, then `test`. Run `debug` first for a bug. No grilling, no doc. |
| Medium | One feature, one session | `grill-me`, `build`, `test`, `review`. Keep the outcome in chat or a short note. |
| Large | Multi-session feature, new project | All seven stages. |
| Hotfix | Production is failing | `debug`, `build` (regression test first), `test`, `review`. Wait for your approval of the fix before `build`. |

### Router

`ask-hammad` is read-only and user-invoked. It asks a few questions about the task, names the size, and prints the path with the real skill names. It is the only place that maps stage names to skills, so there is no `define` skill.

## Decisions

| Decision | Chosen | Rejected |
| --- | --- | --- |
| Base system | Pocock's mechanics plus Osmani's stage names | Osmani whole: skills auto-activate and gates are fixed. Pocock whole: no ship stage. |
| Invocation | Manual only | Model-invoked helpers like Pocock's `tdd` and `grilling`. You want no automatic loading. |
| Artifact home | Repo files, tracker optional | Hardcoding GitHub issues or Basecamp. |
| Weight | Four paths, chosen by you | One fixed pipeline. |
| Interview method | Only `grill-me` interviews. `design` writes up the grilling and does not ask its own questions. | Copy the method into each skill. Share a file: per-skill installs would miss it. |
| `idea` | Untouched for now. You are not using it. | Rework or cut it in this round. |
| `write-a-prd` | Cut. `design` covers it. | Keep both. |
| `model-check` | Stays, manual only | Run at every phase. |
| `ship` | Later | Add now. |
| Stage names | Seven: define, design, plan, build, verify, review, ship | Osmani's six. It merges problem and solution into "define". |
| `define` skill | None. `ask-hammad` maps the stage to `grill-me`. | A `define` skill that duplicates `grill-me`. |
| `design` name | Keep | Rename to `spec`. |

## Requirements

1. All skills except `idea` set `disable-model-invocation: true` and have an `argument-hint`.
2. `design` has no interview section. It writes `docs/<feature>/design.md` from the `grill-me` conversation in the same session. If there is no grilling in context, it says "run `/grill-me` first" and stops.
3. `write-a-prd` is deleted. No doc or skill points to it.
4. `ask-hammad` exists and matches the four paths above (small, medium, large, hotfix). It reminds you to run `design` in the same session as `grill-me`.
5. `skills/model-check` wording no longer says "every new task and every new phase".
6. No skill file contains the word "Basecamp", "GitHub issue" or another tracker name, except as an example in the tracker docs.
7. `README.md` and `docs/choosing-a-skill.md` match the new set. The four paths appear in one place only. Other docs link to it.

## Out of scope

- The `ship` skill.
- Model-invoked helper skills.
- Tracker integrations.
- `idea`, in any way, including its flags and its inline interview.
- Rewriting skill bodies beyond what the requirements list.

## Test strategy

- Grep every `SKILL.md` frontmatter except `idea` for both fields.
- Run `design` in a fresh session with no grilling and confirm it stops with "run `/grill-me` first".
- Grep the repo for `write-a-prd` and tracker names.
- Run `ask-hammad` against five sample tasks and check it returns the right size.
- Run `npx skills add` from a clean directory and confirm 14 skills install.

## Open questions

1. **Docs sweep (does not block).** `new-feature.md`, `debugging.md`, `workflows.md` and others still mention `model-check` as a first step. Plan to review each one when the skills change.
