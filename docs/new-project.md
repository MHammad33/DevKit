# New project

Step-by-step guide for starting a project from an idea. Do each step in order.

## Before you start

You need a validated idea — an `IDEA.md` with **Decision: pursue**, or equivalent clarity. If you only have a rough idea, start with [new-idea.md](new-idea.md) first.

You do not need a repo yet.

Open this guide from the [README](../README.md) when you are ready to turn a pursued idea into a project.

Worked example (support agent, all steps): [workflows.md](workflows.md#own-product-from-vague-idea-full-walkthrough).

For what clarity you gain at each stage—and where it lives—see [from-scratch.md](from-scratch.md).

---

## Step 1 — Write PROJECT.md

**Do**

1. Copy [`templates/PROJECT.md`](../templates/PROJECT.md) into a local folder for your project.
2. Fill in every section. Be specific about v1 scope and constraints.
3. Use the **Constraints** section for technical choices you have already made.

**Result**

A local `PROJECT.md` that describes what you are building and what v1 means.

**Next**

Step 2.

---

## Step 2 — Create the repository

**Do**

1. Create a new Git repository (GitHub or other host).
2. Add `PROJECT.md` as the first commit.

**Result**

A remote repo with your project brief in version control.

**Next**

Step 3.

---

## Step 3 — Install skills

**Do**

1. Follow [install.md](install.md) to install skills from this repository.
2. Confirm skills are available in your agent tool.

**Result**

Skills such as `understand`, `design`, and `build` are ready to use in any project.

**Next**

Step 4.

---

## Step 4 — Add AGENTS.md

**Do**

1. Clone the new repository locally.
2. Copy [`templates/project-AGENTS.md`](../templates/project-AGENTS.md) to `AGENTS.md` in the repo root.
3. Fill in stack, commands, and conventions.
4. If commands are not known yet, write `TBD` and update after scaffolding.

**Result**

Agents working in this repo know how to run tests and follow your conventions.

**Next**

Step 5.

---

## Step 5 — Decide if you need design

**Ask**

Are framework, persistence, auth, hosting, and other technical choices already written in `PROJECT.md` **Constraints**?

| Answer | What to do |
| --- | --- |
| **Yes** | Skip design for now. Go to Step 6. |
| **No** | Run the **grill-me** skill, then the **design** skill for v1. Wait for your approval. Then go to Step 6. |

**Example prompt**

```text
Use the grill-me skill. Read PROJECT.md and stress-test the technical choices for v1.
```

Then:

```text
Use the design skill. Write up the v1 technical decisions from the grilling.
```

**Result**

Either an approved design or a clear path forward without one.

**Next**

Step 6.

---

## Step 6 — Scaffold the project

**Do**

1. Create the minimal app structure for v1.
2. Use **build** if you want the agent to scaffold, or scaffold manually.

**Example prompt**

```text
Use the build skill. Scaffold the minimal app described in PROJECT.md.
```

**Result**

A runnable project skeleton in the repo.

**Next**

Step 7.

---

## Step 7 — Update AGENTS.md

**Do**

1. Replace any `TBD` commands with real dev, test, and lint commands.
2. Commit the updated `AGENTS.md`.

**Result**

Agents can run the correct commands in this repo.

**Next**

Step 8.

---

## Step 8 — Build v1

**Do**

1. Implement v1 scope from `PROJECT.md` (and approved design if you wrote one).
2. Use **build**, then **test**.
3. Use **review** if the change is non-trivial.

**Example prompt**

```text
Use the build skill. Implement v1 from PROJECT.md.
```

**Result**

v1 behavior works and is verified.

**Next**

You are in normal project mode. Use [Start here](../README.md#start-here) for the next situation (feature, debugging, improve).

---

## Quick reference

```text
IDEA
 → Engineering Compass → this guide
 → PROJECT.md (local, then first commit)
 → create repo
 → install skills
 → AGENTS.md
 → design? (only if constraints are not settled)
 → scaffold
 → update AGENTS.md
 → build → test → review (if needed)
```

For worked examples after setup, see [workflows.md](workflows.md).
