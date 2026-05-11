# PRD-001: Multi-Channel Blog Content Pipeline

**Status:** Approved
**Date:** 2026-04-05
**PB:** [PB.md](./PB.md)
**DD:** [DD.md](./DD.md)

## Summary
Write a single markdown doc (`blog-pipeline.md`) that defines the canonical article format, per-channel transformation rules, and a pre-publish review checklist. Validate the rules by running them against two recent articles. Stub the future distribution agent.

---

## Build checklist

> This checklist is the PRD. Work it top to bottom.

### Setup
- [ ] Pick the doc's home: `blog-pipeline.md` at the workspace root (decided in PRD review — keeps it discoverable; can move later if it grows)
- [ ] Pull the design-system component reference into a side window — it's the input to the transformation table

### Build — write the doc
- [ ] Section 1: **Canonical format** — one paragraph defining the main site's article format as source of truth
- [ ] Section 2: **Per-channel transformation table** — rows for site, Substack, LinkedIn, X, Reddit; columns for "what stays / what gets stripped / what gets rewritten / format target (word count, tone)"
- [ ] Section 3: **Pre-publish review checklist** — component enrichment pass, structure check (H2/H3 hierarchy, hook in first two sentences, one thesis), channel readiness (identify the X-tweetable insight, the LinkedIn hook line, the Reddit-worthy takeaway), mobile QA per existing checklist, frontmatter check
- [ ] Section 4: **Distribution agent stub** — one paragraph describing what a future automation could do, marked "deferred — will get its own PB"
- [ ] Decide: channel-specific frontmatter hints (`linkedin_hook`, `x_thread_first_tweet`)? — keep it OUT of v1; add later if friction emerges

### Test — validate against real articles
- [ ] Pick two recently-published articles
- [ ] Run each through the transformation table for Substack and LinkedIn
- [ ] Confirm the rules produce a publishable draft without ad-hoc judgment calls
- [ ] If a step requires the author to "use their judgment," tighten the rule or document the judgment heuristic

### Test — review checklist usability
- [ ] Run the pre-publish checklist on one new article being prepared for publish
- [ ] Time how long the checklist takes — target: under 10 minutes
- [ ] If any step is skipped or feels redundant, cut it

### Deploy
- [ ] Commit `blog-pipeline.md`
- [ ] Add a one-line link to it in the workspace's main `CLAUDE.md` (so future Claude sessions know to consult it before publishing)

### Verify in production
- [ ] Use the pipeline on the next 2–3 articles published
- [ ] After the third use, decide: rules stable enough to write the distribution agent? If yes, draft the agent's PB.

### Document
- [ ] Update workspace `CLAUDE.md` with a one-line pointer to the pipeline doc
- [ ] Note the new doc in the next session log

---

## Out of scope
- Building the distribution agent (deferred — needs its own PB once rules are validated)
- Auto-posting via API (Typefully, Substack, LinkedIn) — would be part of the agent's PRD, not this one
- Updating existing articles to match the new format

## Risks
- **Risk:** Transformation rules don't survive contact with the next article (edge cases not anticipated). → **Mitigation:** the test step requires running against two real articles before deploy. If they break, fix the rules before declaring done.
- **Risk:** Author skips the checklist under deadline pressure. → **Mitigation:** keep the checklist short (target: under 10 minutes). If it grows, cut steps.

## Rollback
Delete `blog-pipeline.md` and revert the `CLAUDE.md` pointer line. Two-minute reversal.
