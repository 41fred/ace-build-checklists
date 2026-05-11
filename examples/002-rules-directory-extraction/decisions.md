# Decisions Log — 002 Rules Directory Extraction

Chronological notes on decisions made during PRD review. Newest first.

## 2026-03-10 — PRD review
- **Open question from DD ("Should client rules use numbers like `90-`?"):** Decided no. Unprefixed names avoid accidental collisions and make it obvious which files came from the operator vs the client.
- **Open question from DD ("Do we need a `_README.md` in `.claude/rules/`?"):** Decided yes, but small — one paragraph explaining the convention. Added to the build checklist as a stretch task.
- **Reviewer pushback on "verify each file is self-contained":** initially vague. Added concrete check: each rule file should be readable on its own without `CLAUDE.md` for context.

## 2026-03-09 — DD review
- **Originally proposed grouping rules into 2 files (logging + behavior):** rejected. Smaller files are easier to update independently. Cost of more files is acceptable.
- **Considered making rules client-customizable via overrides:** deferred to a future PRD if clients ask for it. Avoid premature flexibility.
