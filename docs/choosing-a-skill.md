# Choosing a skill

Use this page when you need a **skill name** or handoff. For the full workflow for a situation, open **Start here** on the [README](../README.md#start-here) instead:

- [New idea](new-idea.md)
- [New project](new-project.md)
- [New feature](new-feature.md)
- [Debugging](debugging.md)
- [Improve](improve.md)

**Invoke any skill by name:**

```text
Use the debug skill. The add button does nothing when clicked.
```

---

## I have X — which skill?

| Situation | Start skill | Typical path |
| --- | --- | --- |
| I am starting a new task or phase | `model-check` | model-check → the skill for the task |
| I have a rough own-product idea | `idea` | [new-idea.md](new-idea.md) |
| I have a validated idea (pursue) | — | [new-project.md](new-project.md) |
| I am adding a feature | — | [new-feature.md](new-feature.md) |
| I need to explore code first | `understand` | understand → design or build |
| I need to design a feature | `design` | design → **approve** → plan or build |
| Design is approved | `plan` or `build` | plan → build → test **or** build → test |
| I know what to build | `build` | build → test |
| Something is broken | `debug` | [debugging.md](debugging.md) |
| Production is failing | `debug` | [debugging.md](debugging.md) |
| I changed code | `test` | test → review (if non-trivial) |
| I want another pair of eyes | `review` | review → build (if fixes needed) |
| Code works but feels messy | `improve` | [improve.md](improve.md) |

---

## After each step

| You just finished | Do this next |
| --- | --- |
| `model-check` | Confirm, then run the skill for the task |
| `idea` (pursue) | Write `PROJECT.md` → [new-project.md](new-project.md) |
| `idea` (pivot) | Re-run **idea** or edit `IDEA.md` |
| `idea` (kill) | Stop |
| `understand` | **design** (choices exist) or **build** / **debug** (clear path) |
| `design` | **Wait for your approval**, then **plan** or **build** |
| `plan` | **build** task 1 → **test** |
| `build` | **test** |
| `test` (all pass, non-trivial) | **review** |
| `debug` | **Approve fix**, then **build** → **test** |
| `improve` | **test** |
| `review` (fix required) | **build** → **test** → **review** again if needed |

---

## When to skip a step

| Step | Skip when |
| --- | --- |
| understand | Exact change is obvious |
| design | Constraints and scope are already in `PROJECT.md` or chat |
| plan | Single-step work |
| review | Trivial one-line fix |
| debug | Cause and fix are obvious |

---

## How to use this in a real project

1. **New idea:** follow [new-idea.md](new-idea.md). Run **idea** → `IDEA.md` → pursue → [new-project.md](new-project.md).
2. **New project:** copy [templates/PROJECT.md](../templates/PROJECT.md) before creating the repo. Copy [templates/project-AGENTS.md](../templates/project-AGENTS.md) after.
3. **Existing project:** pick a skill from the table above and run it in the project repo.
4. **Project artifacts stay in the project:** `IDEA.md` (local, pre-repo), `PROJECT.md`, `AGENTS.md`, `docs/<feature>/design.md`.
5. **This repo stays portable:** principles here, project facts in each project.

---

## Typical paths (short)

**Small bug**

```text
debug → build → test
```

**New feature**

```text
understand → design → approve → plan → build → test → review
```

**Messy working code**

```text
understand → improve → test
```

More detail: [workflows.md](workflows.md).
