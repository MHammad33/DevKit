# Plan: Workflow v2

Design: [design.md](design.md). Tick a task when its "Done when" holds.

Repo state at planning time: 14 skills. `unslop` already has `disable-model-invocation`. `grill-me`, `unslop` and `model-check` have no `argument-hint`. `write-a-prd` appears only in `README.md` and `docs/choosing-a-skill.md`. A grep found no `model-check` mentions in `new-feature.md`, `debugging.md` or `workflows.md`.

## Tasks

- [x] **Task 1: Make every skill except `idea` manual-only**
  - Goal: Add `disable-model-invocation: true` and an `argument-hint` to the frontmatter of the 12 skills that lack one or both. Reword the `model-check` description so it no longer says "every new task and every new phase". Leave `idea` alone.
  - Files likely touched: `skills/{build,craft,debug,design,grill-me,improve,model-check,plan,review,test,understand,unslop}/SKILL.md`
  - Done when: A grep of every `SKILL.md` except `idea` finds both fields. No `model-check` text says "every new task and every new phase". `idea` has no diff.
  - Depends on: none

- [x] **Task 2: Make `design` write up the grilling and stop without one**
  - Goal: Remove any interview section from `design`. It writes `docs/<feature>/design.md` from the `grill-me` conversation in the same session. With no grilling in context, it says "run `/grill-me` first" and stops.
  - Files likely touched: `skills/design/SKILL.md`
  - Done when: `design` has no interview section. In a fresh session with no grilling, `/design` stops with "run `/grill-me` first". With grilling in context, it writes the doc.
  - Depends on: Task 1

- [x] **Task 3: Swap `write-a-prd` for `ask-hammad`**
  - Goal: Delete `skills/write-a-prd`. Create `skills/ask-hammad/SKILL.md` as a read-only, manual-only router. It asks a few questions, names the size (small, medium, large, hotfix) and prints the path with real skill names. It reminds you to run `design` in the same session as `grill-me`. It is the only place that maps stage names to skills. It names no tracker.
  - Files likely touched: `skills/write-a-prd/` (delete), `skills/ask-hammad/SKILL.md` (new)
  - Done when: `ask-hammad` returns the right size and path for five sample tasks (at least one per size). `skills/` holds 14 skills. No skill file names a tracker.
  - Depends on: Task 1

> Milestone: the skill set is final. Docs are what's left.

- [ ] **Task 4: Update docs and README**
  - Goal: Make `README.md` and `docs/choosing-a-skill.md` match the new set. Remove `write-a-prd`, add `ask-hammad`, and show the four paths in one place only (`docs/choosing-a-skill.md`). Other docs link to that place. Add the one-line `Tracker:` convention for a project's `AGENTS.md`, as the only tracker mention outside examples.
  - Files likely touched: `README.md`, `docs/choosing-a-skill.md`, `AGENTS.md` if it carries the tracker line
  - Done when: A grep for `write-a-prd` returns hits only in `docs/workflow-v2/`. A grep for `Basecamp` or `GitHub issue` finds nothing in `skills/`. The four paths are written out in one file only.
  - Depends on: Task 3

- [ ] **Task 5: Docs sweep and install check**
  - Goal: Re-grep `docs/` for `model-check` as a first step and for stale references to removed or changed skills. Fix what turns up. Then run `npx skills add` from a clean directory.
  - Files likely touched: `docs/new-feature.md`, `docs/debugging.md`, `docs/workflows.md`, others only if the grep hits
  - Done when: The sweep finds no stale references. The install lists 14 skills.
  - Depends on: Tasks 1–4
  - Note: the earlier grep found nothing, so this may end with no edits. If so, fold it into Task 4.

## Next

Start with Task 1: use the build skill. Add `disable-model-invocation: true` and an `argument-hint` to every skill except `idea`, and reword the `model-check` description.
