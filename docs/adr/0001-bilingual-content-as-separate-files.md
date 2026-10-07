# ADR-0001: Bilingual Content as Separate Files

**Date**: 2026-10-07  
**Status**: Accepted  
**Context**: Schach-Sport serves a bilingual audience (German + English) and wants to make translation and maintenance manageable. Two main patterns were considered.

## Problem

How should English and German versions of physiology content coexist in the repository?

## Options Considered

1. **Side-by-side in one file**: One Markdown file with EN and DE sections interspersed or stacked
   - ✅ Single source of truth per topic
   - ❌ Harder for translators to work independently
   - ❌ Easy for EN/DE versions to drift in quality or accuracy
   - ❌ Readers jump back and forth between languages

2. **Separate files per language** (chosen): `sleep.en.md` + `sleep.de.md` in the same folder
   - ✅ Translators work independently; no git conflicts
   - ✅ Each language optimized for native speakers (idioms, examples, pacing)
   - ✅ Easy to see which topics are translated (or not yet)
   - ✅ Readers stay in one language
   - ❌ Risk of drift: EN updates don't automatically update DE
   - ❌ Requires a tracking mechanism (frontmatter metadata) to track parity

3. **Folder per language**: `/en/sleep.md` + `/de/sleep.md`
   - ✅ Completely segregated, no confusion
   - ❌ Harder to see relationships between EN/DE pairs
   - ❌ Not obviously better tooling than separate files

## Decision

**Separate files per language (`sleep.en.md` + `sleep.de.md`), colocated in the same folder.**

### Why

- Translators can work independently without git conflicts
- Each language can be optimized for its culture (examples, references, humor)
- Frontmatter metadata (updated dates, author, status) makes parity trackable
- Simple to implement; no build step required

### Trade-off Accepted

**Risk**: EN and DE versions will occasionally drift (EN updated, DE not yet). **Mitigation**: Frontmatter tracks the EN date + DE date. Readers and maintainers can see at a glance which language is stale.

## Consequences

- Content structure: `/content/<category>/topic.en.md` + `/content/<category>/topic.de.md`
- Each file starts with YAML frontmatter: `en_updated: YYYY-MM-DD`, `de_updated: YYYY-MM-DD`, `parity_status: in-sync|de-needs-update|en-needs-update`
- Reviewers check: "Is the EN version current?" → update DE frontmatter to match if translated
- No automated sync; manual discipline required
