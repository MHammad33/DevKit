# Workflows

Short worked examples. For step-by-step guides, use **Start here**:

- [New idea](new-idea.md)
- [New project](new-project.md)
- [New feature](new-feature.md)
- [Debugging](debugging.md)
- [Improve](improve.md)

Skill name lookup: [choosing-a-skill.md](choosing-a-skill.md).

Each example lists: situation, starting skill, path, and what done looks like.

---

## Own product from vague idea (full walkthrough)

**Situation**

Hammad has a vague own-product idea: *"Let's build a customer support agent."* No repo, no stack, no clarity yet.

**Start with**

`idea` — see [new-idea.md](new-idea.md)

**Path**

```text
idea → [pursue / pivot / kill] → PROJECT.md → repo → skills + AGENTS.md
 → design → [approve] → scaffold → AGENTS.md update → build → test → review
```

**Guides**

- Ideation: [new-idea.md](new-idea.md)
- Project bootstrap: [new-project.md](new-project.md)
- Clarity map: [from-scratch.md](from-scratch.md)

### Step 1 — Run the idea skill

**Prompt**

```text
Use the idea skill. Let's build a customer support agent.
```

**Output**

`IDEA.md` locally. Agent proposes answers (marked as assumptions where needed) and recommends **pursue**, **pivot**, or **kill**.

**Example `IDEA.md` highlights**

| Section | Example content |
| --- | --- |
| User | Support agent at a small e-commerce shop (~10–50 orders/day) |
| Problem | Tickets and order details live in different places |
| Product | Inbox where each ticket shows linked order context |
| Will someone pay? | Unknown — validate with shop-owner conversations |
| v1 | Login, ticket list, ticket detail + order, mark resolved |
| Decision | **pursue** — build a demo and talk to 5 shop owners |

**Not yet:** repo, `PROJECT.md`, stack, code.

### Step 2 — Review and decide

Hammad reads `IDEA.md` and agrees: **pursue**.

| Decision | Next |
| --- | --- |
| kill | Stop |
| pivot | Re-run **idea** with a narrower scope |
| pursue | Step 3 |

### Step 3 — Write PROJECT.md

Open [new-project.md](new-project.md) Step 1. Copy from `IDEA.md` into [`templates/PROJECT.md`](../templates/PROJECT.md).

**Example `PROJECT.md` highlights**

| Section | Example content |
| --- | --- |
| One-line | Support inbox for small e-commerce shops — tickets linked to order context |
| Problem | Support agents switch between email and order systems; context gets lost |
| Users | Support agent at a shop doing ~10–50 orders/day |
| v1 scope | Login · ticket list · ticket detail with order info · mark resolved |
| Out of scope | AI replies, Shopify integration, customer chat, billing |
| Constraints | *(empty — stack not chosen)* |
| Done when | Agent can log in, open a ticket, see order details, mark it resolved |

**Not yet:** repo, code.

### Step 4 — Create the repository

Create GitHub repo `support-inbox`. First commit: `PROJECT.md` only.

### Step 5 — Install skills

```bash
npx skills add MHammad33/hammad-engineering
```

Confirm `idea`, `design`, `build`, and other skills are available in the agent tool.

### Step 6 — Add AGENTS.md

Clone locally. Copy [`templates/project-AGENTS.md`](../templates/project-AGENTS.md) → `AGENTS.md`. Use `TBD` for stack and commands until after scaffold.

### Step 7 — Design v1

`PROJECT.md` **Constraints** is empty → run **grill-me**, then **design**.

**Prompt**

```text
Use the grill-me skill. Read PROJECT.md and stress-test the technical choices for v1.
```

Then:

```text
Use the design skill. Write up the v1 technical decisions from the grilling.
```

**Output**

`docs/support-inbox/design.md` — e.g. Next.js + TypeScript + SQLite, simple auth, seeded fake tickets/orders, login → list → detail pages.

**Not yet:** approved, scaffold, code.

### Step 8 — Approve design

Hammad reads the design and replies **approved**. No scaffold or build before this.

### Step 9 — Scaffold

**Prompt**

```text
Use the build skill. Scaffold the minimal app described in PROJECT.md and docs/support-inbox/design.md.
```

**Output**

Runnable skeleton: app structure, dependencies, page shells, seed data. App starts locally.

### Step 10 — Update AGENTS.md

Replace `TBD` with real stack and commands (e.g. `npm run dev`, `npm test`, `npm run lint`). Commit.

### Step 11 — Build, test, review v1

**Prompts**

```text
Use the build skill. Implement v1 from PROJECT.md.
```

```text
Use the test skill. Verify v1 against PROJECT.md Done when criteria.
```

```text
Use the review skill.
```

Fix required review findings → **build** → **test** again.

**Done when**

- Agent can log in, see tickets, open ticket with order details, mark resolved
- Tests pass or are honestly marked unverified
- Review findings addressed or accepted

**After v1**

Normal project mode. Next change → [new-feature.md](new-feature.md).

**Skip**

- **design** — only if `PROJECT.md` **Constraints** already settles stack, auth, and hosting
- **plan** — v1 fits one build pass
- **idea** — if you already have **Decision: pursue** in `IDEA.md`

---

## Small bug

**Situation**

A button stopped working in an existing project. The app is otherwise set up.

**Start with**

`debug` (or `understand` if the cause is likely obvious)

**Path**

```text
debug → [approve fix if needed] → build → test
```

**Example prompt**

```text
Use the debug skill. The "Add task" button does nothing when clicked.
```

**Skip**

design, plan, review (unless the fix is large or risky)

**Done when**

The button works and relevant tests pass or are honestly marked unverified.

---

## New feature

**Situation**

You want Google sign-in on an existing app. Real choices exist: OAuth flow, sessions, env vars.

**Start with**

`design`

**Path**

```text
understand (if needed) → grill-me → design → [wait for approval] → plan (if multi-step) → build → test → review
```

**Example prompt**

```text
Use the grill-me skill. Add Google sign-in. Read PROJECT.md and existing auth code first.
```

Then:

```text
Use the design skill.
```

**Output**

`docs/google-auth/design.md` in the project repo.

**After approval**

- Multi-step work: `Use the plan skill. Break down the approved design.`
- Simple work: `Use the build skill. Implement the approved design.`

**Done when**

Sign-in works, tests pass, and review findings are addressed or accepted.

---

## Production bug

**Situation**

Users get 500 errors when uploading videos. Cause unknown. Urgent.

**Start with**

`debug`

**Path**

```text
debug → [wait for approval on fix] → build → test
```

**Example prompt**

```text
Use the debug skill. Users get 500 errors on video upload. Here are the logs: ...
```

**Rules**

- Do not rewrite large areas before root cause is known.
- Prefer the smallest fix that addresses the cause.

**Skip**

design, plan (unless the fix becomes a large project)

**Done when**

Upload works, cause is documented, and verification evidence is reported.

---

## Messy but working code

**Situation**

A module works but is hard to maintain. No behavior change requested.

**Start with**

`improve`

**Path**

```text
understand → improve → test
```

**Example prompt**

```text
Use the improve skill. Simplify src/upload-handler without changing behavior.
```

**Skip**

design, plan (unless refactor scope grows)

**Done when**

Code is clearer and tests prove behavior is preserved.

---

## Design approved — what next?

**Situation**

You approved `docs/<feature>/design.md` and need to continue.

**Start with**

`plan` or `build`

**Decision**

| Condition | Next skill |
| --- | --- |
| Several independent steps or multiple sessions | `plan` |
| One clear implementation pass | `build` |

**Example prompts**

```text
Use the plan skill. Break the approved design into ordered tasks.
```

```text
Use the build skill. Implement the approved design in docs/google-auth/design.md.
```

---

## Vague request

**Situation**

You said "add authentication" without naming a skill or scope.

**Agent behavior (AGENTS.md)**

1. State that scope is unclear.
2. Run `understand` on existing code.
3. Recommend `design` if choices exist.
4. Ask before `build`.

**You can override**

Use the README table and invoke a skill directly when you already know the path.

---
