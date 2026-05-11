# DD-002: Rules Directory for Governance Separation

**Status:** Approved
**Date:** 2026-03-09
**PB:** [PB.md](./PB.md)

## Before state
Today, every workspace has a single `CLAUDE.md` that mixes project context and behavioral governance. The file averages 350+ lines. Governance topics (logging conventions, access boundaries, session discipline, code modification policy) sit in section headers throughout the file, intermixed with project-locations tables and agent inventories.

When governance improves, the operator manually edits `CLAUDE.md` in each workspace. There's no separation between operator-shipped rules and workspace-specific additions, so every update risks a merge conflict.

## After state
`CLAUDE.md` keeps project context only — locations tables, agent inventories, naming conventions, plus a short paragraph pointing at the rules directory.

A new `.claude/rules/` directory contains one file per behavioral concern. Files are number-prefixed (`01-temp-logging.md`, `02-access-boundaries.md`, etc.) for predictable ordering. Claude Code auto-loads every `.md` file in this directory on session start.

When governance improves, the operator updates the relevant rule file and propagates it to client workspaces independently of `CLAUDE.md`. Client-added rules use unprefixed filenames, so operator and client files never collide.

## Visual: before → after
- [`DD-before.html`](./DD-before.html) — single CLAUDE.md mixing both concerns
- [`DD-after.html`](./DD-after.html) — CLAUDE.md (context) + .claude/rules/ (governance), with arrows showing how updates flow

> Generated as standalone HTML files using inline SVG + CSS. Open in a browser.

## Design considerations
- **Picked `.claude/rules/` over `.claude/governance/` or similar:** `.claude/rules/` is Claude Code's native auto-load location. Anything else would require explicit reads, defeating the always-active property.
- **Picked number prefixes for operator files (`01-`, `02-`...):** gives a stable namespace. Client files stay unprefixed, so the two never conflict alphabetically. Numbers are *not* a load-order signal — Claude Code treats all rule files as equal-weight context.
- **Picked one rule per file over grouped rules:** smaller files are easier to update independently and easier for the AI to weight correctly. The cost is more files to manage; we judged that acceptable.
- **Picked a one-paragraph pointer in `CLAUDE.md` over no pointer:** without it, a human reading `CLAUDE.md` for the first time has no idea governance lives elsewhere. The pointer is documentation for humans, not Claude.

## Open questions
- [ ] Should client-added rules also use numbers (e.g., starting at `90-`)? — Decide in PRD. Current lean: no, unprefixed avoids accidental collisions.
- [ ] Do we need a `_README.md` inside `.claude/rules/` explaining the convention? — Decide in PRD.

---

> **Next stage:** PRD with build checklist.
