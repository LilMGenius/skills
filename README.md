# Skills For Fake Engineers

The agent skills I actually use, shared so you can too.

## Quickstart

> Run with administrator/elevated privileges so skills are symlinked, not copied, and stay auto-updating.

```bash
npx skills@latest add LilMGenius/skills --global --agent '*'
```

## Reference

### Productivity

**Model-invoked**

- **[re0](./skills/productivity/re0/SKILL.md)** — Refresh an existing artifact after a session: clean up, sync up, dedupe, and rewrite it into the current best v0.
- **[ssotchk](./skills/productivity/ssotchk/SKILL.md)** — Audit where one fact is duplicated or scattered across artifacts and platforms; report the canonical source of truth and a consolidation plan (read-only).
- **[ssotize](./skills/productivity/ssotize/SKILL.md)** — Consolidate a scattered fact into one canonical home and replace the rest with references (mutating).

`ssotchk` / `ssotize` work breadth-first across many places; `re0` works depth-first on one artifact — pair them, and once a fact is cleanly SSOT'd, maintain it with `re0`.

## Credits

Built on the architecture and philosophy of [mattpocock/skills](https://github.com/mattpocock/skills) (MIT) — these are LilMGenius's own, non-overlapping workflows, **not a fork**. A few shared building blocks are vendored verbatim; see [NOTICE](./NOTICE). Authoring conventions: [CLAUDE.md](./CLAUDE.md).
