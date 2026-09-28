# Eval item: issue-08

- source: zulip/zulip#39794
- captured: 2026-08-05
- calibration: false

## Repo facts (captured 2026-08-05)

- repo: zulip/zulip (25604 stars, archived: no)
- description: Zulip server and web application. Open-source team chat that helps teams stay productive and focused.
- last push to any branch: 2026-08-04
- latest release: 12.1 (2026-06-26)
- open issues + PRs: 2043
- last 5 default-branch commits:
  - 2026-08-03 by amanagr: tornado: Report errors as JSON instead of rendering portico pages.
  - 2026-08-03 by amanagr: test_tornado: Run the test harness with Tornado's URL configuration.
  - 2026-08-03 by PieterCK: webhook/slack: Handle missing "real_name" field in UserInfo endpoint.
  - 2026-07-29 by sathwikshetty33: webhooks/airbyte: Remove stale STREAM_NAME attribute.
  - 2026-07-14 by sathwikshetty33: webhooks/docs: Advise collecting only necessary fixtures.
- maintainer first-response sample (5 recently updated issues, days to first owner/member/collaborator comment):
  - #38839 (opened 2026-04-06 by a maintainer): 91.7 days
  - #39859 (opened 2026-07-31): 2.6 days
- contribution policy (CONTRIBUTING.md, section "AI use policy and guidelines"): AI tools allowed; contributors must personally understand, test, and be able to explain every change; AI-generated PRs that appear untested or not understood are closed without review
- this issue: assignees: piyushagarwal-55; linked PRs: zulip/zulip#39811 (open)

## Issue

### Migrate compose and message-edit banners to the modern banner component (#39794)

opened by Yogesh-Shivaji365 (COLLABORATOR) on 2026-07-21, state open, labels: help wanted, good first issue, area: message-editing, in progress, area: compose (banners & validation), area: compose

The compose box and message-edit banners still use the legacy `.main-view-banner` markup, instead of the modern banner component
(`web/src/banners.ts`, viewable in the development environment at http://localhost:9991/devtools/banners/).

Because the legacy close button is an `<a role="button" tabindex="0">`, it takes focus on mouse clicks and shows a focus outline. That was worked around in #39759 with a `:focus:not(:focus-visible)` rule and a TODO pointing here; migrating would let us drop the workaround.

Note that the two components use different layout systems (flexbox vs. CSS grid, different padding, line height, and close button size), so this will change how the banners look worth confirming the intended [design](https://chat.zulip.org/#narrow/channel/101-design) before implementing.

## Comments (8 total, first 8 shown)

[comments truncated - see original fetch for details]
