# Contributing to Schach-Sport

This guide explains how to write and contribute content topics to Schach-Sport.

## Content Structure

All physiology topics live under `/content/<category>/`, organized by subject:

```
content/
├── exercise-movement/        # Yoga, Qigong, breathing, stretching
├── sleep/                    # Sleep cycles, recovery, tournament sleep
├── nutrition/                # Diet, hydration, meal timing
├── mental-resilience/        # Stress management, focus, pressure handling
└── hydration-immune-health/  # Hydration, immune system, illness prevention
```

## Writing a Topic

### 1. Create a Bilingual Pair

Each topic exists in two files:
- `topic-name.en.md` (English)
- `topic-name.de.md` (German)

They live in the same folder.

### 2. Use This YAML Frontmatter

Every topic file starts with metadata:

```yaml
---
title: "Sleep for Chess Performance"  # English title
de_title: "Schlaf für Schachleistung"  # German title
author: "Your Name"
en_updated: 2026-10-07
de_updated: 2026-10-07
parity_status: "in-sync"  # in-sync | de-needs-update | en-needs-update
tags:
  - sleep
  - tournament
  - recovery
sources:
  - "Smith et al. (2022). Sleep and Cognitive Performance in Chess. Journal of Sports Science."
  - "https://example.com/chess-sleep-study"
---

# Sleep for Chess Performance
```

**Parity status legend**:
- `in-sync`: Both EN and DE versions are current with each other
- `de-needs-update`: English was updated; German translation is outdated
- `en-needs-update`: German was updated; English translation is outdated

When you update a topic, update the corresponding `*_updated` date and `parity_status`.

### 3. Follow This Loose Template

Not required, but recommended for consistency:

```markdown
## Overview

Why does this matter for chess? 1–2 paragraphs setting the stakes.

## The Science

What does research say? Cite sources. Assume your audience knows chess but not physiology.

## Practical Tips

Concrete advice. Bullet points or numbered steps. Age-appropriate for teens/young adults.

### Common Mistakes

What do people get wrong about this?

## Video Resources

If relevant, link to videos (as your current README does).

## Sources & Further Reading

Full citations. Links to papers, books, etc.
```

## Review Process

1. **Create a GitHub issue** with title: `Topic: <topic name>`
   - Body: Brief description of what the topic covers
   - Label: `needs-triage`

2. **Respond to clarification** if needed
   - Maintainer might ask: scope, audience level, special considerations
   - Label will move to `needs-info` → `ready-for-agent` or `ready-for-human`

3. **Create a branch and PR**
   - Branch name: `content/category/topic-name`
   - PR title: `#<issue-number> — <topic name>`
   - Link to the issue in the PR description

4. **Request review** from maintainer
   - Reviewed for: accuracy (science), clarity (writing), bilingual parity (if both EN/DE present)

5. **Merge and close**
   - Once approved, maintainer merges and closes the issue

## Example Topic

See `content/exercise-movement/yoga-morning-routine.en.md` for a complete example.

## Questions?

Ask on the issue tracker or contact the maintainer.
