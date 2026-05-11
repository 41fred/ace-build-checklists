# Decisions Log — 001 Multi-Channel Blog Content Pipeline

Chronological notes on decisions made during PRD review. Newest first.

## 2026-04-05 — PRD review
- **Open question from DD ("Channel-specific frontmatter hints?"):** Decided no for v1. Adding hints up front is premature optimization. Author can derive hooks at distribution time; if that proves repetitive, add them later.
- **Open question from DD ("Where does the doc live?"):** Decided top-level `blog-pipeline.md`. Discoverability beats neatness. Can move to `Web Services/` later if a folder-of-related-docs emerges.
- **Reviewer pushback on "use the pipeline on next 2–3 articles":** initially said "use it once." Bumped to 2–3 to actually surface edge cases. Once is not a real test.

## 2026-04-04 — DD review
- **Originally proposed building the distribution agent in this same PRD:** rejected. The whole point of the manual checklist is to validate rules before automating. Build the agent in a follow-up PB once rules are stable.
- **Considered making the canonical format spec strict (schema + linter):** deferred. v1 is a doc, not a tool. Schema enforcement only earns its keep if the doc gets ignored.
