# CLAUDE.md snippet

> Paste this block into your workspace's `CLAUDE.md` to teach Claude how to work the build process. Put it after your project structure section, before any "Rules" section.

---

## Build Process

This workspace uses a four-stage pipeline: **PB → DD → PRD → Build**.

**Location:** `Ace-Build-Process/` (or wherever you placed it)
- `_templates/` — `PB.md`, `DD.md`, `PRD.md`
- `NNN-feature-name/` — one folder per feature, contains the docs for that feature
- `index.html` — tracks every proposal and its current stage

**Read `Ace-Build-Process/README.md` before building an app, shipping a feature, or changing a meaningful internal process.**

### Session rules

1. Before starting any build or process change, check `index.html` for an existing proposal.
2. If there's no proposal and the work qualifies (see table below), **draft a PB first** — never self-approve, always wait for the user.
3. Once the PB is approved, recommend a DD unless the implementation path is obvious. The user decides whether to skip.
4. After the DD (or PB if DD was skipped), write the PRD as a **build checklist**, not as prose. The checklist is the centerpiece.
5. When implementing, open the PRD and work the checklist top to bottom. Mark items `[x]` as you finish, `[N/A]` for skipped steps (with reason).
6. Update `index.html` whenever a stage advances.

### When the pipeline applies

| Use the pipeline | Just build it |
|------------------|---------------|
| Building a new app or feature | Bug fixes |
| New integration or external dependency | Typos, copy edits |
| Changing a meaningful internal process | Dependency version bumps |
| Architecture or schema change | One-line config changes |
| Anything that affects users or downstream systems | Routine maintenance |
