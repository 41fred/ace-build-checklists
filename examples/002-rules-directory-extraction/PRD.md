# PRD-002: Rules Directory for Governance Separation

**Status:** Approved
**Date:** 2026-03-10
**PB:** [PB.md](./PB.md)
**DD:** [DD.md](./DD.md)

## Summary
Extract behavioral rules from `CLAUDE.md` into `.claude/rules/`. Ship four starter rule files. Update `CLAUDE.md` to keep project context only and add a pointer paragraph. Verify auto-load in a fresh session.

---

## Build checklist

> This checklist is the PRD. Work it top to bottom.

### Setup
- [ ] Create branch `feature/002-rules-directory`
- [ ] Confirm Claude Code version supports `.claude/rules/` auto-load (run a quick test: drop a dummy `99-test.md` with one sentence, restart, ask Claude what's in it)

### Build — extract rules
- [ ] Create directory `.claude/rules/`
- [ ] Create `.claude/rules/01-temp-logging.md` — copy temp-logging section from `CLAUDE.md` verbatim, no edits
- [ ] Create `.claude/rules/02-access-boundaries.md` — copy access-boundaries section verbatim
- [ ] Create `.claude/rules/03-session-discipline.md` — copy session-discipline section verbatim
- [ ] Create `.claude/rules/04-code-modification.md` — copy code-modification section verbatim
- [ ] Verify each file is self-contained (no broken references to surrounding `CLAUDE.md` context)

### Build — update CLAUDE.md
- [ ] Remove the four extracted sections from `CLAUDE.md`
- [ ] Add a "Rules" section pointing at `.claude/rules/`:
  ```
  ## Rules
  Always-active behavioral rules live in `.claude/rules/`. These files are
  loaded automatically by Claude Code on every session. Add new behavioral
  conventions there, not here.
  ```
- [ ] Verify `CLAUDE.md` line count dropped meaningfully (target: under 200 lines)

### Test — single workspace
- [ ] Restart Claude Code in this workspace
- [ ] In a new session, ask: "What's our temp logging convention?" — Claude should answer correctly without re-reading `CLAUDE.md`
- [ ] Ask: "What's our code modification policy?" — same check
- [ ] Confirm Claude doesn't quote stale text from a now-removed `CLAUDE.md` section

### Test — packager template
- [ ] Update workspace-packager to copy `.claude/rules/` into new client workspaces
- [ ] Update the client `CLAUDE.md` template to include the Rules pointer paragraph
- [ ] Generate a test client workspace, verify rules load on first session

### Deploy
- [ ] Merge `feature/002-rules-directory` to `main`
- [ ] Push the rules directory to one canary client repo (low-risk client first)
- [ ] Verify on the client: open a fresh session, ask the same temp-logging and code-modification questions, confirm correct answers
- [ ] Roll out to remaining clients

### Verify in production
- [ ] Two weeks after rollout, check at least one session log per client to confirm temp logs match the convention (proxy for "the rule is being followed")
- [ ] Check that no client's `CLAUDE.md` was clobbered during rollout — git diff each one against pre-rollout

### Document
- [ ] Update root `CLAUDE.md` Rules table to list the four shipped rules
- [ ] Update workspace-packager docs to describe the rules-directory packaging step
- [ ] Add an entry to the changelog

---

## Out of scope
- Adding new rules beyond the four extracted (we're moving existing rules, not authoring new ones)
- Per-client custom rules (clients can add unprefixed files later; not part of this PRD)
- Tooling to validate rule-file format or detect drift (future PRD if needed)

## Risks
- **Risk:** Claude Code's auto-load behavior changes in a future version. → **Mitigation:** the rules are still readable as plain markdown; if auto-load breaks, we add explicit `Read` instructions in `CLAUDE.md` as a fallback.
- **Risk:** A client has already customized their `CLAUDE.md` and the diff-and-patch overwrites their changes. → **Mitigation:** review each client's current `CLAUDE.md` before pushing; merge customizations forward, never overwrite.

## Rollback
Move the four rule files' contents back into `CLAUDE.md`, delete `.claude/rules/`, redeploy. ~15 minutes per workspace.
