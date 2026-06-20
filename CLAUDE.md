# LilMGenius Skills

The authoring guide for these skills — itself a skill artifact, so `re0` it when it drifts. Live catalog: [README](./README.md).

## Philosophy

**Composable, single-responsibility skills that sharpen the work — including this repo itself.** Every skill is general enough to use *while building the skills*, so authoring is **recursive and self-improving**: we maintain the skills with the skills. Treat that loop as the point.

**Single Source of Truth.** One fact lives in exactly one place; everything else references it by name. Skills invoke each other in prose, never by copying content or reaching into another skill's files.

**Two vectors.** `re0` works depth-first (one artifact → clean v0); `ssotchk`/`ssotize` work breadth-first (one truth across many). Establish order with SSOT, then keep it with `re0` rather than re-consolidating.

## Repository layout

```
skills/<perspective>/<name>/SKILL.md
```

Organize by **artifact perspective**, not topic: `single/` works on the one artifact in hand (`re0`, `re0-git`, `shower`, `tasting`); `cross/` reconciles one truth across many (`ssotchk`, `ssotize`). Topic domains belong in *separate plugins*, so the only durable cut within a plugin is artifact perspective — add a bucket only when the reason is clear and durable. One skill = one directory with a `SKILL.md`; keep drafts and retired skills out of the README and `plugin.json`.

## SKILL.md format

```
---
name: <kebab-name>            # matches the directory and the invocation
description: "<trigger-rich one-liner>"
---

<one line: what the skill does>

## Goal
## Workflow      — numbered steps
## Rules         — constraints / what not to do
## Verification  — checks before finishing; report what changed
```

## Invocation

Every `SKILL.md` is either user-invoked (`disable-model-invocation: true`, reachable only by the human) or model-invoked (model- or user-reachable). For the taxonomy, description conventions, and why a user-invoked skill can invoke model-invoked skills but never another user-invoked one, see [docs/invocation.md](./docs/invocation.md). *(vendored verbatim; see Vendoring & lineage)*

**The dividing line.** Default to **model-invoked**. Make a skill **user-invoked** only when the model should *never* reach it on its own — its trigger or effect is a deliberate, human-decided action (committing, pushing, publishing, deploying), or having it in reach would bias the agent toward one. Such a skill can't be composed, so it also stays out of `tasting`. Today only `re0-git` qualifies (it cleans a *commit's* message — committing is human-decided); everything else is model-invoked and composable.

## Shipping a change

Before committing:

1. **SKILL.md** — new/changed skill follows the format above.
2. **README.md** — list every active skill, grouped into Model-invoked and User-invoked, each linked to its `SKILL.md`.
3. **.claude-plugin/plugin.json** — register each active skill's path.
4. **package.json** — bump version (new skill = minor; fix/docs/refactor = patch); keep `keywords` grouped logically (identity → agents → capabilities).
5. **tasting** — run it (`shower` + `ssotchk` + `re0`) before finalizing.

Commit messages: Conventional Commits, one bullet per real change — no padding, no mechanical trivia (version bumps, file registration), no co-author tags. `re0-git` restores a drifted message to this.

## Vendoring & lineage

Not a fork of [mattpocock/skills](https://github.com/mattpocock/skills) — we adopt its architecture and philosophy and ship our own non-overlapping workflows, vendoring only the small shared substrate so the repo stays *our skills plus clearly-credited building blocks*.

Reused material stays **verbatim**, credited in [NOTICE](./NOTICE) **per source** (project + license + copyright), not per file — never paraphrase to drop credit. Add a source block there the first time you vendor from a source; later material needs none.
