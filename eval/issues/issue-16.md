# Eval item: issue-16

- source: conda/conda#16487
- captured: 2026-08-05
- calibration: false

## Repo facts (captured 2026-08-05)

- repo: conda/conda (7481 stars, archived: no)
- description: A system-level, binary package and environment manager running on all major operating systems and platforms.
- last push to any branch: 2026-08-04
- latest release: 26.7.0 (2026-07-31)
- open issues + PRs: 662
- last 5 default-branch commits:
  - 2026-08-04 by codewithdaniel1: docs: add authenticated channels guide (#16483)
  - 2026-08-04 by danyeaw: Recipe: add conda-rattler-solver as a run dependency (#16491)
  - 2026-08-04 by codewithdaniel1: docs: update commands concept page (#16485)
  - 2026-08-04 by codewithdaniel1: docs: update channels concept page (#16484)
  - 2026-08-04 by danyeaw: Docs: Fix plantuml download failures by using conda-forge (#16492)
- maintainer first-response sample (5 recently updated issues, days to first owner/member/collaborator comment):
  - #16275 (opened 2026-06-24 by a maintainer): 32.9 days
  - #16493 (opened 2026-08-04): no maintainer comment in thread
  - #16231 (opened 2026-06-15): no maintainer comment in thread
  - #16023 (opened 2026-05-05): no maintainer comment in thread
  - #16026 (opened 2026-05-05): no maintainer comment in thread
- contribution policy (CONTRIBUTING.md, section "Generative AI"): generative AI tools welcome; you are responsible for all contributions and must review and understand AI-generated content before including it in a pull request
- this issue: assignees: none; linked PRs: none

## Issue

### Conda channel notices break json parsing (when stderr and stdout are on the same pipe) (#16487)

opened by Callek (CONTRIBUTOR) on 2026-08-03, state open, labels: type::bug

### Checklist

- [x] I added a descriptive title
- [x] I searched open reports and couldn't find a duplicate

### What happened?

When a channel notice is active for a used channel, but you specify `--json` output. Such as on a `conda create ...` command, you get the channel notice output as raw text on stderr. where if a user is capturing both stderr and stdout on the same pipe could break json parsing. But also means that the notices are invisible to the json.

[Content truncated - see original fetch for full details]

## Comments (0 total, first 0 shown)

(no comments)
