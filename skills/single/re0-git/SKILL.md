---
name: re0-git
disable-model-invocation: true
description: "Rewrite a finished commit's message into a clean, handoff-ready form — in your own log style — so `git log` alone tells the story, no `git diff` archaeology next session. Run it yourself after a commit (user-invoked on purpose, never auto-fired). Message only: never the tree, always gpg-signed; the commit you finalize takes fresh dates, older commits keep theirs."
---

`re0` for git: rewrite a finished commit's message so the log hands off on its own — in the author's own voice, not an imposed one.

## Goal

Repeated amends and momentum-commits leave a message bloated, stale, or padded with trivia. `re0-git` applies `re0` to the message: a clean version that lets a fresh session continue from `git log` alone, without reading the diff. It refines *what the author already writes* — it never imposes a format, and it never makes a commit. Only the message moves — and timestamps, per the date rule below; the tree never changes.

It is **user-invoked** — you run it once you've decided to commit. Deliberately not model-invoked and not chained from `tasting`: a commit-cleanup tool sitting in the agent's reach would bias it toward committing when it shouldn't, so it's kept out of that reach entirely.

## Workflow

1. Scope the target — usually `HEAD`, sometimes a short unpushed range. A commit must already exist; re0-git never creates one.
2. Read two things: what actually changed (`git show --stat`, `git diff`) so the message is true, and the author's recent `git log` so you match how they write — a one-line head, or a subject with bullets, terse or prose, whatever it is.
3. Rewrite the message in that style, keeping only what carries the change for a handoff. Cut the rest: stale or half-true lines, restated context, and mechanical or derivable trivia (version bumps, file registration, "also updated X"). One point per real change — never pad to a length.
4. Re-commit signed, with dates per the rule below: for the tip you're finalizing (`HEAD`), a plain `git commit --amend -S` lets both dates default to now; to keep an older commit's dates, rebuild it with `GIT_AUTHOR_DATE`/`GIT_COMMITTER_DATE git commit-tree <tree> -p <parent> -S` and move the branch ref. For a range, the tip restamps and the rest preserve.
5. Verify and report.

## Rules

- **Never create or suggest a commit** — re0-git only rewrites the message of a commit that already exists. Using it is never a reason to commit.
- **Message only** — the tree must stay byte-identical (`git diff <old> <new>` empty); never edit content in a re0-git pass.
- **Match the author's style, don't impose one** — no mandated convention, structure, tone, or emoji. Mirror their existing log; a one-line head stays a one-line head.
- **Keep the essence, cut the trivia** — leave only what a fresh session needs to hand off from the log; no padding, no mechanical or derivable noise. The log is the single source of truth for the change.
- **Dates by position; always gpg-signed.** The commit you're finalizing — `HEAD` — takes both author and committer date = now, because re-cleaning the latest commit is itself continued work. Every older commit (`HEAD~1` and back) keeps its original author + committer dates; never restamp the past.
- **Never rewrite pushed or shared history** without explicit confirmation — it forces a force-push.

## Verification

1. `git diff <old-tip> <new-tip>` is empty — content unchanged.
2. Each rewritten commit is gpg-signed (`%G?` = `G`) with dates as intended.
3. `git log` reads clean in the author's own style and is enough for handoff on its own.
