# PB-002: Rules Directory for Governance Separation

**Status:** Approved
**Date:** 2026-03-08
**Author:** Operator

## What we're building
Move always-active behavioral rules out of `CLAUDE.md` into a `.claude/rules/` directory of small, focused files that Claude Code auto-loads on every session.

## Problem
`CLAUDE.md` mixes two concerns that grow at different rates:
1. **Project context** — what is this project, where do files live, how is the structure organized.
2. **Behavioral governance** — how the AI should behave (logging conventions, access boundaries, code modification policy, session discipline).

Project context changes when the project changes. Governance rules accumulate over time as new failure modes are discovered. The result is that `CLAUDE.md` is now 350+ lines, and the longer it gets, the more likely the AI deprioritizes any individual rule.

A second pain: when a governance rule improves, propagating it to every workspace requires editing `CLAUDE.md` in each one, which risks merge conflicts with workspace-specific customizations.

## Solution
Create `.claude/rules/` containing one file per behavioral concern (`01-temp-logging.md`, `02-access-boundaries.md`, `03-session-discipline.md`, `04-code-modification.md`). Claude Code auto-loads everything in this directory on every session, so these stay always-active without further config. `CLAUDE.md` keeps only project context plus a one-paragraph pointer to the rules directory.

## Why this solution
- **Granular updates:** improving one rule only touches one small file — no risk of clobbering project context.
- **Distribution:** rule files can be propagated across workspaces independently of each workspace's `CLAUDE.md`.
- **Cognitive load:** smaller, focused files are easier for both humans and AI to scan and weight correctly.

The trade-off we're accepting: an additional folder to maintain, and one more place to look when debugging a rule.

## Approaches considered
- **Keep everything in `CLAUDE.md`:** Rejected — current state. Doesn't scale, makes cross-workspace updates painful.
- **Use `.claude/settings.json`:** Rejected — settings is for tool permissions, not behavioral rules. Wrong abstraction.
- **One mega-file `CLAUDE-governance.md`:** Rejected — Claude Code only auto-loads `CLAUDE.md` and `.claude/rules/*`, not arbitrary files. Would require explicit reads.
- **Symlink shared rules from a central operator workspace:** Rejected — fragile across machines, breaks in git-distributed clients.
- **Chosen — `.claude/rules/` directory:** the solution above.
