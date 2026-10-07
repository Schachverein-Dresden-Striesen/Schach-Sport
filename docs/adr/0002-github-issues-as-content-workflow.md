# ADR-0002: GitHub Issues as Content Workflow

**Date**: 2026-10-07  
**Status**: Accepted  
**Context**: Schach-Sport is a curated content repository owned by a small team. We need a lightweight workflow to track topics from idea → drafted → reviewed → published.

## Problem

What mechanism tracks a content topic's lifecycle (idea → draft → review → merge)?

## Options Considered

1. **Direct commits to main**: Author writes, team reviews in Discord/email, commits directly
   - ✅ Minimal overhead; fastest path for small team
   - ❌ No visible history; no ticket-based tracking; easy to lose ideas
   - ❌ Doesn't use the triage/ready-for-agent labels already set up

2. **GitHub Issues + Pull Requests** (chosen): Each topic is an issue. Author creates branch → PR. Triage labels track state.
   - ✅ Transparent progress; audit trail
   - ✅ Integrates with triage labels (`needs-triage`, `ready-for-agent`, `ready-for-human`)
   - ✅ Blocks on dependencies (if topic B requires topic A to be published first)
   - ✅ Scales to multiple maintainers and eventual agents
   - ❌ Slightly more overhead than direct commits

3. **Separate issue tracker (Jira, Linear, etc.)**: Decouple content planning from code
   - ❌ Overkill for a small team; another tool to maintain
   - ❌ Doesn't live in the repo

## Decision

**GitHub Issues + PRs, using the five triage roles (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`).**

### Workflow

1. **Idea phase**: Author creates a GitHub issue with a topic title and initial scope. Label: `needs-triage`.
2. **Clarification**: If team needs more info from author, add `needs-info`. Author responds as a comment.
3. **Spec ready**: Maintainer (you, for now) confirms scope and acceptance criteria. Label: `ready-for-agent` or `ready-for-human`.
   - `ready-for-agent`: Topic can be written by an AI agent (well-scoped prompt in issue body)
   - `ready-for-human`: Topic requires human expertise (specialist trainer, personal experience)
4. **Implementation**: Author/agent creates a branch and opens a PR (linked to the issue). PR title: `#<issue> — <topic name>`.
5. **Review**: Maintainer reviews for accuracy and clarity (EN) and bilingual parity (if DE also complete). Iterate in PR comments.
6. **Publish**: Maintainer approves and merges to main. Closes the issue.

### Labels Used

- `needs-triage`: New issue, not yet scoped
- `needs-info`: Waiting on author clarification
- `ready-for-agent`: Fully specified, AI-ready
- `ready-for-human`: Requires domain expert; scope is clear
- `wontfix`: Out of scope or duplicate

### Why

- Aligns with Matt Pocock's triage/ready-for-agent workflow (reduces friction with future agent-driven content)
- Transparent progress visible to the whole team
- Scales: as you add a second maintainer or AI agents, the workflow doesn't change
- Issues can block each other (if topic B depends on topic A being published first)

## Consequences

- All content ideas live as GitHub issues
- Small overhead for team: each topic ≈ 1 issue + 1 PR
- Clear definition of "done": issue closed, PR merged, on main
- Future AI agents can read the issue and PR to understand intent + feedback

## When This Might Change

- If the team grows large (20+ contributors) and needs heavyweight project management
- If you eventually move to a static site generator that needs different metadata/build steps
