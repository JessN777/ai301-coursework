# Eval item: issue-14

- source: LegalQuants/lq-ai#490
- captured: 2026-08-05
- calibration: false

## Repo facts (captured 2026-08-05)

- repo: LegalQuants/lq-ai (113 stars, archived: no)
- description: 
- last push to any branch: 2026-08-05
- latest release: desktop-v0.6.2 (2026-07-04)
- open issues + PRs: 133
- last 5 default-branch commits:
  - 2026-08-05 by SaifAlYounan: Scope autonomous retrieve_chunks to the session owner (AG-01, Refs #288) (#401)
  - 2026-08-05 by sergiomaldo: List KBs by the project_knowledge_bases junction, with backfill (#442)
  - 2026-08-04 by SaifAlYounan: Derive ProviderEgressRefused from LQAIError (typed per CONTRIBUTING) (#488)
  - 2026-08-03 by SaifAlYounan: Guard LLM provider base_url egress at build time (GW-04, Refs #288) (#400)
  - 2026-08-01 by SaifAlYounan: Validate project ownership on chat creation (API-01 IDOR, Refs #288) (#397)
- maintainer first-response sample (5 recently updated issues, days to first owner/member/collaborator comment):
  - #489 (opened 2026-08-04): no maintainer comment in thread
- contribution policy (CONTRIBUTING.md): no statement on AI or contribution tooling
- this issue: assignees: none; linked PRs: none

## Issue

### Docs: remove Discord references — the server was never stood up (#490)

opened by houfu (CONTRIBUTOR) on 2026-08-04, state open, labels: documentation, good first issue

## Summary

Our issue templates and contributor docs point people at a Discord server (`discord.gg/lq-ai`) that doesn't exist — it was planned in the original repo-opening checklist but never created. Anyone who clicks the link today hits a dead invite.

The fix is to remove the Discord references and route community conversation to **GitHub Discussions**, which we do keep open for questions from outside the LegalQuants team (and which SECURITY.md and ADR 0022 already rely on).

This is a documentation-only change — no code, no tests, no build step. It's a good first contribution if you'd like to get familiar with our PR process.

## What to change

Six files reference Discord. In each, remove the Discord reference and, where it served as a "where to ask" pointer, point at GitHub Discussions instead:

[Detailed instructions in original fetch]

## Comments (0 total, first 0 shown)

(no comments)
