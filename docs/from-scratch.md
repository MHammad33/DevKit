# From scratch: clarity at each stage

How Engineering Compass turns a vague idea into a project you can build from. This guide documents **what clarity you have**, **where it lives**, and **how you know you are ready to move on**.

For the step-by-step checklist, use [new-project.md](new-project.md). For skill names and handoffs, use [choosing-a-skill.md](choosing-a-skill.md).

---

## What this platform is

Engineering Compass is a **workflow**, not a web app or issue tracker.

| Layer | What it is | Where you find it |
| --- | --- | --- |
| **Guides** | Step-by-step paths for common situations | This repo, `docs/` |
| **Skills** | Focused agent instructions for one phase | Installed in your agent tool; source in `skills/` |
| **Project artifacts** | Facts about *your* project | Your repo: `PROJECT.md`, `AGENTS.md`, `docs/<feature>/` |
| **Agent policy** | Rules all agents follow | Root `AGENTS.md` in this repo; copy `templates/project-AGENTS.md` into your project |

You do not log in anywhere. You read the guide, run skills in chat, and review artifacts in your project repo.

---

## The clarity ladder

Each stage answers a different kind of question. Do not skip a rung unless the guide says you can.

```text
Stage 0  IDEATE         → Should we build this? (IDEA.md)
Stage 1  PROJECT.md     → What is v1, and what is not?
Stage 2  REPO           → Where does the project live?
Stage 3  SKILLS         → How do we work with agents?
Stage 4  AGENTS.md      → How do agents run and behave in this repo?
Stage 5  DESIGN         → How will we build it technically?
Stage 6  SCAFFOLD       → What does the codebase look like?
Stage 7  AGENTS.md (v2) → What commands and conventions are real?
Stage 8  BUILD + VERIFY → Does v1 actually work?
```

After v1, clarity for new work follows [new-feature.md](new-feature.md): understand → design → approve → plan? → build → test → review.

---

## Stage 0 — Ideate (no repo)

**You have:** a rough idea, maybe one sentence.

**You lack:** validated problem, user, value, money story, and a go/no-go decision.

**What to do:** follow [new-idea.md](new-idea.md). Run the **idea** skill. Write `IDEA.md`.

**Clarity you gain:**

| Question | Answered in IDEA.md |
| --- | --- |
| What pain does this solve? | Problem |
| Who is it for? | Users |
| Why build this? | Motivation |
| What exactly is the product? | Product, How it works |
| Will anyone pay? | Money |
| What is v1? | Smallest useful version |
| Should we build this? | Decision (pursue / pivot / kill) |
| When do we stop? | Kill criteria |

**Artifact:** `IDEA.md` (local, before any repo).

**Ready for Stage 1 when:** you agree with **Decision: pursue** in `IDEA.md`.

---

## Stage 1 — Write PROJECT.md

**You have:** an idea worth pursuing.

**You lack:** a shared, versioned brief that agents and humans can read.

**What to do:**

1. Copy [`templates/PROJECT.md`](../templates/PROJECT.md) into a local folder.
2. Fill every section. Be specific about v1 scope and out-of-scope items.
3. Put settled technical choices in **Constraints**. Leave **Constraints** empty if framework, persistence, auth, or hosting are still open.

**Clarity you gain:**

| Question | Answered in |
| --- | --- |
| What problem are we solving? | **Problem** |
| Who is this for? | **Users** |
| What must work in v1? | **v1 scope** |
| What are we explicitly not building yet? | **Out of scope (v1)** |
| What choices are already made? | **Constraints** |
| How will we know v1 is finished? | **Done when** |

**Artifact:** `PROJECT.md` (local file, not yet in git).

**Ready for Stage 2 when:** every section has real content—not placeholders—and **Done when** items are observable (you could check them yes/no).

**Still unclear after this stage:** technical architecture (unless **Constraints** is complete), folder structure, commands, implementation order.

---

## Stage 2 — Create the repository

**You have:** a written brief.

**You lack:** a canonical home for the project and its history.

**What to do:**

1. Create a new Git repository.
2. Commit `PROJECT.md` as the first commit.

**Clarity you gain:**

| Question | Answered? |
| --- | --- |
| Where is the source of truth for the project brief? | Yes — repo root `PROJECT.md` |
| Can we track how the brief evolves? | Yes — git history |

**Artifact:** remote repo with `PROJECT.md`.

**Ready for Stage 3 when:** the repo exists and you can clone it locally.

---

## Stage 3 — Install skills

**You have:** a repo with a brief.

**You lack:** a consistent way to invoke agent phases (understand, design, build, etc.).

**What to do:** follow [install.md](install.md) and confirm skills are available in your agent tool.

**Clarity you gain:**

| Question | Answered? |
| --- | --- |
| What skills exist? | understand, design, plan, build, test, review, debug, improve |
| How do I invoke one? | `Use the <skill> skill. <context>` |
| Which guide matches my situation? | [README Start here](../README.md#start-here) |

**Artifact:** skills installed in your environment (not in the project repo).

**Ready for Stage 4 when:** you can run a skill by name in chat.

---

## Stage 4 — Add AGENTS.md

**You have:** a repo, skills, and a product brief.

**You lack:** project-specific instructions for how agents should work in *this* repo.

**What to do:**

1. Clone the repo locally.
2. Copy [`templates/project-AGENTS.md`](../templates/project-AGENTS.md) to `AGENTS.md` in the repo root.
3. Fill in stack, commands, and conventions where known.
4. Write `TBD` for commands not known until after scaffolding.

**Clarity you gain:**

| Question | Answered in |
| --- | --- |
| What stack are we using? | **Stack** (or TBD) |
| How do we run dev, test, lint? | **Commands** (or TBD) |
| What patterns must agents follow? | **Conventions** |
| What needs extra care? | **Sensitive areas** |
| What does done mean in this repo? | **Done for this repo** |

**Artifact:** `AGENTS.md` in your project repo.

**Ready for Stage 5 when:** `AGENTS.md` is committed. It is OK if commands are still `TBD`.

**Still unclear:** exact technical design (if **Constraints** in `PROJECT.md` is empty or incomplete).

---

## Stage 5 — Design (conditional)

**Decision gate:** read `PROJECT.md` **Constraints**.

| **Constraints** status | What to do |
| --- | --- |
| Framework, persistence, auth, hosting, and other major choices are written | Skip design for now. Go to Stage 6. |
| One or more major choices are missing or marked TBD | Run the **grill-me** skill, then the **design** skill for v1. Wait for your approval. |

**Example prompt:**

```text
Use the grill-me skill. Read PROJECT.md and stress-test the technical choices for v1.
```

Then:

```text
Use the design skill. Write up the v1 technical decisions from the grilling.
```

**What to do after design is written:**

1. Read `docs/<feature>/design.md` (or the chat design for tiny changes).
2. Reply **approved**, or request changes and re-run design.

**Clarity you gain:**

| Question | Answered in design |
| --- | --- |
| How does v1 work end to end? | **Proposed approach** |
| What did we choose and reject? | **Decisions** |
| What must the implementation satisfy? | **Requirements** |
| What must not break? | **Invariants** |
| What happens when things fail? | **Error behavior** |
| How will we verify it? | **Test strategy** |
| What is explicitly excluded? | **Out of scope** |
| What is still unresolved? | **Open questions** |

**Artifact:** `docs/<feature>/design.md` with status awaiting approval → approved.

**Ready for Stage 6 when:** either (a) constraints were already complete in `PROJECT.md`, or (b) design is **approved** by you.

**Do not scaffold or build before approval** when design was required.

---

## Stage 6 — Scaffold the project

**You have:** approved product scope and settled technical direction.

**You lack:** a runnable codebase.

**What to do:**

1. Create the minimal app structure for v1.
2. Use **build** if you want the agent to scaffold, or scaffold manually.

**Example prompt:**

```text
Use the build skill. Scaffold the minimal app described in PROJECT.md.
```

**Clarity you gain:**

| Question | Answered? |
| --- | --- |
| What folders and entry points exist? | Yes — repo tree |
| Does the app start or run a smoke path? | Yes/no — run it |
| What dependencies does the project use? | Yes — package files, lockfiles |

**Artifact:** runnable project skeleton in the repo.

**Ready for Stage 7 when:** you can run the dev server or equivalent and the project structure matches the approved design or constraints.

---

## Stage 7 — Update AGENTS.md (second pass)

**You have:** a scaffold with real commands.

**You lack:** accurate agent instructions tied to the actual toolchain.

**What to do:**

1. Replace `TBD` entries in **Commands** with real dev, test, and lint commands.
2. Update **Stack** and **Conventions** if scaffolding revealed gaps.
3. Commit the updated `AGENTS.md`.

**Clarity you gain:**

| Question | Answered? |
| --- | --- |
| How does an agent run tests in this repo? | Yes — exact commands |
| What conventions match the scaffold? | Yes — updated **Conventions** |

**Artifact:** `AGENTS.md` with no `TBD` commands.

**Ready for Stage 8 when:** an agent (or you) can run dev and test commands successfully from the repo root.

---

## Stage 8 — Build, test, and review v1

**You have:** brief, agent instructions, design (if needed), and a skeleton.

**You lack:** working v1 behavior with evidence.

**What to do:**

1. Implement v1 scope from `PROJECT.md` (and approved design if you wrote one).
2. Run **build**, then **test**.
3. Run **review** if the change is non-trivial.

**Example prompts:**

```text
Use the build skill. Implement v1 from PROJECT.md.
```

```text
Use the test skill. Verify v1 against PROJECT.md "Done when" criteria.
```

**Clarity you gain:**

| Question | Answered? |
| --- | --- |
| Does v1 behave as specified? | Yes — tested against **Done when** |
| What passed, failed, or is unverified? | Yes — test skill output |
| Are there review findings to fix? | Yes — review skill output (if run) |

**Artifacts:** working code, test results, optional review notes in chat.

**Ready for normal project mode when:** **Done when** criteria in `PROJECT.md` are met or honestly marked unverified with reason.

---

## Clarity map: one page

| Stage | Primary artifact | You can answer |
| --- | --- | --- |
| 0 Ideate | `IDEA.md` | Should we build this? Why? For whom? |
| 1 PROJECT.md | `PROJECT.md` | What is v1? What is not? When is it done? |
| 2 Repo | git remote | Where does the project live? |
| 3 Skills | installed skills | Which agent phase do I run next? |
| 4 AGENTS.md | `AGENTS.md` v1 | How should agents behave in this repo? |
| 5 Design | `docs/<feature>/design.md` | How will we build it? What did we decide? |
| 6 Scaffold | codebase | What does the project look like on disk? |
| 7 AGENTS.md | `AGENTS.md` v2 | What exact commands do agents run? |
| 8 Build + verify | code + test output | Does it work? |

---

## How to visit this when you are stuck

| If you are wondering… | Open |
| --- | --- |
| What step am I on? | This guide — find the stage whose "Still unclear" list matches your questions |
| What do I do next mechanically? | [new-project.md](new-project.md) |
| Which skill should I run? | [choosing-a-skill.md](choosing-a-skill.md) |
| What does a full path look like in practice? | [workflows.md](workflows.md) |
| What are the agent rules? | [AGENTS.md](../AGENTS.md) in this repo; your project's `AGENTS.md` for repo facts |

**Quick self-check:** if you cannot point to the artifact that holds an answer, you are probably not far enough along the ladder for that question yet.

---

## After v1: adding features

Clarity for new work in an existing project follows a shorter ladder:

```text
understand  → What exists today? What will this touch?
design      → How should this feature work? (approve before build)
plan?       → What order do we implement in? (skip if one pass)
build       → Working code
test        → Evidence against acceptance criteria
review      → Second pair of eyes on non-trivial changes
```

Full guide: [new-feature.md](new-feature.md).

---

## Principles

- **Clarity has a location.** If it is not in `PROJECT.md`, `AGENTS.md`, an approved design, or verified test output, treat it as unsettled.
- **Product clarity before technical clarity.** `PROJECT.md` before design, unless constraints are already complete.
- **Approval is a gate.** After **design**, you must approve before **plan** or **build**.
- **Evidence closes the loop.** **Done when** in `PROJECT.md` is only real after **test** (or an honest unverified mark).
- **Skip steps only when the guide allows it.** Empty **Constraints** means design. Single-step work means skip plan. Obvious one-line fixes mean skip review.
