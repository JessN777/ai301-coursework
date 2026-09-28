# Eval item: issue-15

- source: zulip/zulip#19589
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
- this issue: assignees: none; linked PRs: zulip/zulip#20840 (closed); zulip/zulip#23123 (closed)

## Issue

### Separate `command` and `text` field for slack-compatible outgoing webhook (#19589)

opened by esamson (NONE) on 2021-08-18, state open, labels: help wanted, area: integrations, good first issue

Discussed here: https://chat.zulip.org/#narrow/stream/127-integrations/topic/gitlab.20slash.20commands/near/1247658

Current behavior puts entire message, including bot mention, in the `text` field of the outgoing POST.

POST coming from Slack itself puts the "slash command" in a separate `command` field while their `text` field only contains the message body after the command.

For better compatibility, if message starts with a bot mention then we should separate that out into a `command` field and put the rest of the message in the `text` field.

Perhaps we can also transform the mention (`**@mybot**`) to a slash command (`/mybot`) so it looks like it would coming from Slack.

## Comments (97 total, first 40 shown)

[comments truncated - see original fetch for details]
