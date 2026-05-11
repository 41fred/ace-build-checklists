# PRD-NNN: [Feature Name]

**Status:** Draft
**Date:** YYYY-MM-DD
**PB:** [link to PB.md]
**DD:** [link to DD.md, or "skipped"]

## Summary
One paragraph. What's getting built and what "done" looks like.

---

## Build checklist

> **This checklist is the PRD.** Work it top to bottom. Don't skip steps — if one doesn't apply, mark it `[N/A]` and add a one-line reason. The checklist is the deliverable; everything else on this page is supporting context.

### Setup
- [ ] [Specific, runnable action — e.g., "create branch `feature/xxx`"]
- [ ] [Specific, runnable action — e.g., "install dep `foo@^2`"]

### Build
- [ ] [Specific, runnable action with file path or command]
- [ ] [Specific, runnable action with file path or command]
- [ ] [Specific, runnable action with file path or command]

### Test
- [ ] [Verification with expected result — e.g., "run `npm test`, all green"]
- [ ] [Verification with expected result]
- [ ] [Manual check — e.g., "open page X, confirm element Y renders"]

### Deploy
- [ ] [Specific, runnable action — e.g., "merge to main, push to staging"]
- [ ] [Specific, runnable action — e.g., "trigger production deploy"]

### Verify in production
- [ ] [Observable check — e.g., "log line `xxx` appears within 5min of first request"]
- [ ] [Observable check]

### Document
- [ ] [Update README, CLAUDE.md, or relevant docs]
- [ ] [Note in changelog or release notes]

---

## Out of scope
What we are *not* building this round. List explicitly to prevent scope creep.

- [Thing 1]
- [Thing 2]

## Risks
Each risk gets a mitigation. If you can't write a mitigation, the risk is too large for this PRD.

- **[Risk]** → [mitigation]
- **[Risk]** → [mitigation]

## Rollback
How to undo if it goes wrong. One paragraph.
