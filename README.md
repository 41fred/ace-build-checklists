# Build Checklists for Claude Code

A four-stage pipeline for building features without wasting effort on bad ideas, vague designs, or rushed execution.

```
PB  →  DD  →  PRD  →  Build
```

| Stage | What it answers | Output |
|-------|-----------------|--------|
| **PB** (Product Brief) | Should we do this? | One page: what / problem / solution / why this solution / approaches considered |
| **DD** (Design Doc) | What does it look like? | Before/after state, HTML visual charts, design considerations |
| **PRD** (Product Requirements Doc) | How do we get it built well? | A runnable build checklist |
| **Build** | Build it. | Working feature, checklist marked off |

## What it's for

Use this pipeline whenever you're **building an app, shipping a feature, or changing a meaningful internal process** — anything where execution quality matters and skipped steps cost real time.

Don't use it for typos, small fixes, dependency bumps, or one-off config changes. Just do those.

## Why this pipeline

Most building goes wrong in one of three places:
1. **The wrong thing gets built** — fix with the PB.
2. **The right thing is poorly designed** — fix with the DD.
3. **The right thing, well designed, is sloppily executed** — fix with the PRD checklist.

Skip stages when the work is small, but don't skip the PRD checklist. The checklist is what keeps execution honest.

## How to use this repo

1. Copy `_templates/` and (optionally) the `CLAUDE.md-snippet.md` block into your workspace.
2. For each new feature, create a numbered folder: `001-feature-name/`.
3. Drop in `PB.md`, then (if needed) `DD.md`, then `PRD.md`.
4. Track every proposal in `index.html`.

## Stage rules

### PB — keep it tight
A PB is one page. If you can't fit it on one page, the idea isn't clear yet. Skip the PB only for small fixes (typos, dependency bumps, one-line config changes).

### DD — visualize before you spec
The DD's job is to make the new behavior obvious before anyone writes code. Generate **before** and **after** diagrams as HTML files (`DD-before.html`, `DD-after.html`) — inline SVG + CSS, no dependencies. They render anywhere, version cleanly, and update without re-exporting.

Skip the DD when the implementation path is obvious from the PB.

### PRD — checklist over prose
**The PRD is a checklist.** Not a spec doc. Not a design write-up. A list of runnable steps that, when checked off in order, ship the feature.

Why: prose PRDs read like reading material. Checklists are runnable. When you skim a 5-page PRD on a build day, you skip steps. When you tick boxes, you don't.

The supporting context (summary, out-of-scope, risks, rollback) sits below the checklist, not above.

### Build — work the checklist
Open the PRD and work top to bottom. Mark items `[x]` as you finish, `[N/A]` if a step doesn't apply (with a one-line reason). When the last box is checked, the feature ships.

## Flexible usage

| Change size | Pipeline | Example |
|-------------|----------|---------|
| Major | PB → DD → PRD → Build | New product, new app, architecture change |
| Medium | PB → PRD → Build | New integration, internal workflow change |
| Small but significant | PB → Build | Opinionated config change, scoped tweak |
| Small fix | Just build | Bug fix, typo, dep bump, one-line config |

## Naming convention

```
NNN-feature-name/
├── PB.md
├── DD.md            (optional)
├── DD-before.html   (optional)
├── DD-after.html    (optional)
├── PRD.md
└── decisions.md     (optional — captures changes during review)
```

Use the next available ID from `index.html`.

---

## License

MIT. Use it, fork it, ship it. Copyright © 2026 [Alcanah Partners](https://alcanah.co). Full terms in [`LICENSE`](./LICENSE).

---

## Credits

Build Checklists for Claude Code is built by **[Alcanah Partners](https://alcanah.co)**, founded by **Alfred Naayem**.

Questions, feedback, or stuck on something? Email **alfred@alcanah.co**. Alfred reads everything.
