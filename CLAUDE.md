# PaperThin

The guide for authoring these skills — and itself a skill artifact, so `re0` it when it drifts. The shipped catalog is [README](./README.md).

## Philosophy

- **Trust the artifact, not the author.** A skill exists to make work read true to someone who wasn't there. The maker's in-session mind is the worst judge of whether it does — so a skill either re-derives the work from what's true now, or imports outside eyes to test it.
- **Single source of truth.** One fact lives in one place; everything else references it by name. Skills compose by naming each other in prose — never by copying content or reaching into another skill's files. Shared material lives in its owning skill; others point to it.
- **Restraint.** Change only what genuinely improves — a pass that finds nothing to improve changes nothing. The enemy is slop (noise, duplication, padding), not addition.
- **Recursive.** Every skill is general enough to use *while building the skills*, so we maintain the skills with the skills, and each pass is audited and refined by the tools it ships. Treat that loop as the point.

## Layout

```
skills/<perspective>/<name>/SKILL.md
```

Group by **artifact perspective** — which is the suite's two vectors made physical:

- `single/` — **depth**: refine or verify the one artifact in hand (`re0`, `re0-git`, `shower`, `tasting`).
- `cross/` — **breadth**: reconcile one truth across many artifacts and platforms (`ssotchk`, `ssotize`).

Reach for `cross/` to *establish* order (legacy refactor, knowledge-base build, fresh scaffolding); once a fact is cleanly SSOT'd, *maintain* it with `re0` rather than re-consolidating. Topic domains belong in separate plugins, so within a plugin the only durable cut is perspective. One skill = one directory with a `SKILL.md`; keep drafts and retired skills out of the README and `plugin.json`.

## SKILL.md format

```
---
name: <kebab-name>            # matches the directory and the invocation
description: "<trigger-rich one-liner>"
---

<one line: what the skill does>

## Goal
## Workflow      — numbered steps
## Rules         — constraints
## Verification  — checks before finishing; report what changed
```

## Invocation

Every `SKILL.md` is either user-invoked (`disable-model-invocation: true`, reachable only by the human) or model-invoked (model- or user-reachable). For the full definitions, description conventions, and why a user-invoked skill can invoke model-invoked skills but never another user-invoked one, see [docs/invocation.md](./docs/invocation.md).

Default to model-invoked. Make a skill user-invoked only when the model should never reach it on its own — its trigger is a deliberate, human-decided action (commit, push, publish, deploy), or its mere presence in reach would bias the agent toward one. A user-invoked skill can't be composed, so it also stays out of `tasting`. Today only `re0-git` qualifies: it cleans a commit's message, and committing is human-decided.

## Shipping

Before committing:

1. **SKILL.md** follows the anatomy above.
2. **README** lists it — grouped Model-/User-invoked, each linked to its `SKILL.md`.
3. **plugin.json** registers its path.
4. **package.json** bumps version (new skill = minor; fix/docs = patch); `keywords` stay grouped logically.
5. Run **`tasting`** — `shower` the artifact, `ssotchk` the repo, `re0` the docs.

Commit messages: Conventional Commits, one bullet per real change — no padding, no mechanical trivia, no co-author tags. `re0-git` cleans a drifted message back to its essence, in the author's own style.

## Vendoring

Not a fork of [mattpocock/skills](https://github.com/mattpocock/skills) — we adopt its architecture and philosophy and ship our own non-overlapping workflows, vendoring only the small shared substrate. Reused material stays **verbatim** and is credited in [NOTICE](./NOTICE) per source (project · license · copyright), never paraphrased to drop credit.
