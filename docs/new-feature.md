# New feature

Step-by-step guide for adding a meaningful feature to an existing project. Do each step in order. Skip only when the table says you can.

## Before you start

You already have a project with `PROJECT.md` and `AGENTS.md`. Skills are installed.

Open this guide from the [README](../README.md) **Start here** section.

---

## Step 1 — Understand the current system

**Do**

1. Run the **understand** skill on the area the feature will touch.
2. Note existing patterns, files, and constraints from `PROJECT.md` and project `AGENTS.md`.

**Example prompt**

```text
Use the understand skill. I want to add Google sign-in. Summarize existing auth and session code.
```

**Result**

A short picture of what exists and what will be affected.

**Next**

Step 2.

---

## Step 2 — Design the feature

**Do**

1. Run the **grill-me** skill first. **design** stops if there is no grilling.
2. Run the **design** skill.
3. Write `docs/<feature-slug>/design.md` in the **project** repo. For a tiny change, skip design and use the small path in `docs/choosing-a-skill.md`.
4. Cover approach, decisions, requirements, test strategy, and out of scope.

**Example prompt**

```text
Use the grill-me skill. Add Google sign-in. Read PROJECT.md and existing auth code first.
```

Then:

```text
Use the design skill. Write up the Google sign-in decisions from the grilling.
```

**Result**

A design ready for your review.

**Next**

Step 3. Do **not** start coding yet.

---

## Step 3 — Approve the design

**Do**

1. Read the design.
2. Reply **approved**, or request changes and return to Step 2.

**Result**

An approved design. The agent must wait for this before **plan** or **build**.

**Next**

Step 4.

---

## Step 4 — Plan or build

**Ask**

Is this more than one focused implementation pass?

| Answer | What to do |
| --- | --- |
| **Yes** — several steps or sessions | Run **plan**, then build tasks one by one |
| **No** — one clear change | Skip plan. Go to Step 5 with **build** |

**Example prompts**

```text
Use the plan skill. Break the approved design into ordered tasks.
```

```text
Use the build skill. Implement the approved design in docs/google-auth/design.md.
```

**Result**

Either an ordered task list, or you move straight into implementation.

**Next**

Step 5.

---

## Step 5 — Build

**Do**

1. Run **build** for the whole feature or for the next plan task.
2. Keep the change as small as the design allows.
3. Do not expand scope without asking.

**Result**

Working code for the scoped change.

**Next**

Step 6.

---

## Step 6 — Test

**Do**

1. Run the **test** skill.
2. Check acceptance criteria from the design.
3. Mark anything unverified honestly.

**Example prompt**

```text
Use the test skill. Verify Google sign-in against the design acceptance criteria.
```

**Result**

Pass, fail, or unverified for each criterion.

**Next**

If tests fail → fix with **build**, then **test** again. If they pass → Step 7.

---

## Step 7 — Review

**Do**

1. Run the **review** skill (fresh subagent).
2. Fix required findings with **build** → **test**.
3. Re-review if the change was large.

**Skip when**

The change is trivial after all (rare for a real feature). Prefer review for auth, data, and security.

**Result**

Findings and a verdict. You decide what to merge.

**Next**

Done for this feature. Use [Start here](../README.md#start-here) for the next situation.

---

## Quick reference

```text
understand
 → design
 → approve
 → plan? (if multi-step)
 → build
 → test
 → review
```

## Principles

- Decide before expensive coding.
- Wait for explicit approval after **design**.
- Prefer the smallest complete change.
- Skip **plan** when one **build** is enough.
- Verify with evidence, then review when it matters.

Skill lookup if you get stuck: [choosing-a-skill.md](choosing-a-skill.md).
