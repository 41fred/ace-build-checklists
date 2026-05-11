# PB-001: Multi-Channel Blog Content Pipeline

**Status:** Approved
**Date:** 2026-04-03
**Author:** Operator

## What we're building
A documented pipeline that turns one canonical article into channel-specific drafts (Substack, LinkedIn, X, Reddit) by following deterministic transformation rules.

## Problem
Articles written for the main site use rich components (callouts, pull quotes, signup forms, figure captions) that don't render anywhere else. Adapting them for other channels is manual: strip components by hand, adjust tone, reformat. The friction is high enough that most articles never get distributed beyond the site, leaving reach on the table.

There's no canonical source-of-truth, no transformation rules, and no review step that checks whether the article uses the full component vocabulary available.

## Solution
Define one canonical format (the site version) and write transformation rules per downstream channel. Ship a one-page pipeline doc that includes the canonical format, per-channel rules in a table, a pre-publish review checklist, and a stub for a future automation agent.

## Why this solution
A pipeline doc is fast to write, immediately usable, and reversible (delete one file). It validates the transformation rules manually before any code gets written — premature automation would encode bad rules.

## Approaches considered
- **Substack as canonical, crosspost to site:** Rejected — Substack's formatting can't represent callouts, signup forms, or custom CSS. The site's vocabulary is richer and should be the source of truth.
- **Single universal markdown (lowest common denominator):** Rejected — defeats the purpose of having a design system. We'd never use the components we built.
- **Build the distribution agent first:** Rejected — need to validate the rules manually on 2-3 articles before automating. Otherwise we encode bad rules in code and refactor later.
- **Chosen — Pipeline doc with manual transformation rules:** the solution above.

