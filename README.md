<div align="center">

# Skills For Fake Engineers

**The agent skills I actually use, shared so you can too.**

Plain-Markdown skills that turn old engineering wisdom into reflexes your agent reaches for on its own — on **any** agent: Claude Code, Codex, Cursor, Antigravity, Grok-Build, Hermes, OpenClaw, Pi, etc.

[Quickstart](#quickstart-15-seconds) · [Reference](#reference) · [The Problem](#the-problem) · [The Fixes](#the-fixes) · [Credits](#credits)

</div>

---

## Quickstart (15 seconds)

1. **Install** for every agent you use:
   ```bash
   npx skills@latest add LilMGenius/skills --global --agent '*'
   ```
2. **Run it elevated** so the skills are symlinked (they auto-update), not copied.
3. **Use them** — model-invoked, so your agent reaches for them on its own; or call one by name, like `/re0`.

**Not sure?** Paste that command into whatever agent you're using and just say "set this up for me" — it'll do the rest.

## Reference

### Model-invoked — your agent reaches for these on its own
| Skill | Scope | What it does |
|---|---|---|
| ♻️ **[re0](./skills/single/re0/SKILL.md)** | one artifact | Rewrite a drifted artifact into a clean v0 — not another patch |
| 🚿 **[shower](./skills/single/shower/SKILL.md)** | one artifact | Cold-read it with fresh, zero-context eyes — does it stand on its own? *(read-only)* |
| 🔎 **[ssotchk](./skills/cross/ssotchk/SKILL.md)** | many artifacts | Find where one fact is scattered or duplicated; name the canonical source *(read-only)* |
| 🧲 **[ssotize](./skills/cross/ssotize/SKILL.md)** | many artifacts | Consolidate it into one home and point the rest at it |
| 🍴 **[tasting](./skills/single/tasting/SKILL.md)** | your output | After any change, auto-runs `shower` + `ssotchk` + `re0` on it |

### User-invoked — you run these yourself
| Skill | Scope | What it does |
|---|---|---|
| 🧾 **[re0-git](./skills/single/re0-git/SKILL.md)** | one commit | Rewrite a finished commit's message into a clean v0 so `git log` alone hands off |

## The Problem

**Most agent skills are slop.**

Point an agent at a goal and it **adds** — more files, more options, more "helpful" boilerplate. Adding looks like progress, and nothing ever makes it go back and delete.

> [!WARNING]
> Repeat that across a project and you get the familiar AI-generated toolkit: near-duplicate skills, dead settings, a README that says the same thing three times. Plausible, busy, and quietly unmaintainable.

These skills bet the other way — **every one of them removes:**

- `re0` rewrites a draft into a clean v0 instead of patching it,
- `ssotchk` / `ssotize` collapse the same fact scattered across files,
- `shower` cuts whatever a stranger can't follow,
- `tasting` runs all of it on your own output, automatically.

> [!TIP]
> The hard part isn't adding features — it's restraint. A pass that finds nothing to improve changes nothing. **That restraint is the product.**

## The Fixes

**Each is a well-worn principle, made automatic.**

### #1 — Artifacts rot
Edit a doc one piece at a time across a session and it bloats: stale deltas, duplicated noise, changelog scars. Patching on top just preserves the rot.

**The fix → `re0`:** rewrite the artifact as a clean v0, as if it were the first version.

> *Prior art: the Boy Scout Rule — "leave it cleaner than you found it" (Robert C. Martin, [Clean Code](https://www.informit.com/articles/article.aspx?p=1235624&seqNum=6), 2008). `re0` goes further: rewrite, don't just tidy.*

<details>
<summary><b>[PROOF]</b></summary>

- **Setup** — we asked `re0` to refresh these docs once more, but they were already at v0.
- **Result** — it changed a single commit date and left every line of prose untouched.
- **So** — a tool that does nothing when nothing is wrong never bloats your repo: these skills remove noise, they never add it.
</details>

### #2 — You go blind to your own work
After a long session you're the one person who *can't* read your own work straight: you know too much, so your brain quietly fills every gap and the holes turn invisible.

**The fix → `shower`:** hand a stranger who never saw your session only the artifact, and ask "does this actually make sense?"

> *Prior art: [egoless programming](https://en.wikipedia.org/wiki/Egoless_programming) — you can't review your own work objectively; someone else must (Gerald Weinberg, 1971). Here, that someone is a context-free sub-session.*

<details>
<summary><b>[PROOF]</b></summary>

- **Setup** — we handed `shower` its own spec, to a sub-session with zero context, holding only the file.
- **Result** — in minutes it found three bugs the author had missed:
  - a step that hinted the answer it should hide,
  - a path that leaked spoiler files,
  - a scope too vague to act on.
- **So** — a skill that catches its own bugs can catch yours.
</details>

### #3 — The same fact ends up everywhere
A timeout value, a decision, a status — copied into a README, a doc, a ticket, and a Slack thread. The copies drift, and now no one knows which is true.

**The fix → `ssotchk` + `ssotize`:** find the scatter, name the canonical source, then consolidate and point the rest at it.

> *Prior art: [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) — one fact, one authoritative home (Hunt & Thomas, The Pragmatic Programmer, 1999).*

### #4 — "Remember to verify" never fires
A guideline buried in docs won't trigger in a brand-new session — exactly when author bias is highest.

**The fix → `tasting`:** the moment you finish something, it runs `shower`, `ssotchk`, and `re0` on your output, automatically.

> *Prior art: [dogfooding](https://en.wikipedia.org/wiki/Eating_your_own_dog_food) — eat your own dog food (Microsoft, 1988). Taste your own cooking before you serve it.*

### #5 — Your session doesn't travel; the git log does
Your session is stuck where it ran — this agent, this account, this machine. A teammate or another agent can't load the context your work happened in.

**The fix → `re0-git`:** clean a finished commit's message so `git log` — the one thing every environment shares — carries the handoff, and anyone picks up from the log alone.

<details>
<summary><b>[PROOF]</b></summary>

- **Setup** — `re0-git`'s very first target was its own release commit.
- **Result** — dogfooding it surfaced two faults, both fixed:
  - a message padded with trivia,
  - a spec that preached "no redundancy" while repeating itself.
- **So** — its first cleanup was after itself.
</details>

## Credits

- **Built on** [mattpocock/skills](https://github.com/mattpocock/skills) (MIT) — its architecture and philosophy.
- **Not a fork** — these are [LilMGenius](https://github.com/LilMGenius)'s own, non-overlapping workflows.
- **Vendored verbatim** — a few shared building blocks, kept as-is with per-source attribution in [NOTICE](./NOTICE).
- **Authoring guide** — conventions and philosophy live in [CLAUDE.md](./CLAUDE.md).
