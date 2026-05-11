# DD-001: Multi-Channel Blog Content Pipeline

**Status:** Approved
**Date:** 2026-04-04
**PB:** [PB.md](./PB.md)

## Before state
The author writes an article in markdown with rich HTML components (callouts, pull quotes, signup forms, figure captions) and publishes it to the main site. To distribute it elsewhere, the author manually:
- Opens the article in a text editor
- Copy-pastes it into Substack and strips the HTML by hand
- Re-writes a 300-word version for LinkedIn from scratch
- Distills the key insight into a Twitter thread, also from scratch
- Sometimes posts to Reddit; sometimes skips it because of effort

There's no shared rule for which components map to what on each channel. Two articles get adapted in two different ways depending on the author's mood. Most articles never make it past the main site.

## After state
The article is still written canonically for the main site. A new doc — `blog-pipeline.md` — sits in the workspace and tells the author exactly how to transform the canonical version for each channel.

The doc has four parts:
1. **Canonical format definition** — what counts as the source of truth.
2. **Per-channel transformation table** — for each channel, what stays, what gets stripped, what gets rewritten.
3. **Pre-publish review checklist** — before publishing the canonical version, run through a component-enrichment pass, structure check, and channel-readiness check.
4. **Distribution agent stub** — a one-paragraph note that a future agent could automate the transformations once the rules have been validated manually.

The author follows the doc when distributing. When a new component is added to the design system (rare), the author updates the transformation table.

## Visual: before → after
- [`DD-before.html`](./DD-before.html) — flowchart showing the author manually transforming for each channel, with friction marks at each step
- [`DD-after.html`](./DD-after.html) — flowchart showing the canonical version flowing through the pipeline doc into channel-specific drafts

## Design considerations
- **Picked the main site as canonical, not Substack:** Substack can't represent custom components; the site has the richest vocabulary. Canonical = whichever format loses the least information.
- **Picked a transformation table over per-channel sub-docs:** one table on one page is faster to scan than four nested docs. The cost is each cell stays terse — that's a feature.
- **Picked a manual checklist over an immediate automation:** the rules need to be validated on 2–3 real articles before encoding them in code. Premature automation locks in bad rules.
- **Picked stubbing the distribution agent in the doc itself:** keeps the future-state visible without committing to it. When it's time to build, the stub becomes the next PB.

## Open questions
- [ ] Should the canonical version include channel-specific hints in frontmatter (e.g., `linkedin_hook: "..."`) — or should the author derive them at distribution time? Decide in PRD.
- [ ] Where does the doc live? Top-level `blog-pipeline.md`, or under a `Web Services/` folder? Decide in PRD.
