# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer responsive | Maintainer first-response sample in repo facts; latency from first issue comment to first maintainer reply | First maintainer response within 30 days of issue creation or most recent activity | required |
| Repo actively maintained | Last 5 default-branch commits and latest release date in repo facts | At least one commit from a human (not bot) within past 6 months | required |
| Repo not archived | Archived flag in repo facts | Repository is not archived; "archived: false" or no archived mention | required |
| Issue is bounded | Issue body and comment thread in the bundle | Issue describes one specific piece of work; not an umbrella issue, tracking issue, or design discussion without a settled direction | required |
| No active blockers on contribution | Contribution policy and AI policy lines in repo facts | Contribution policy does not explicitly ban AI-generated code; conditions like disclosure or testing are acceptable | required |
| No current assignee | Assignees field in repo facts | Issue has no current assignee (strict gate) | required |
| No active linked PR | Linked PRs in repo facts and comment thread | No open pull requests linked to the issue; closed unmerged PRs are resolved | required |
| Issue has clear acceptance criteria | Issue body and comment thread | Issue describes what "done" looks like (acceptance criteria, expected behavior, or clear problem statement) | preferred |
| Good-first-issue label | Issue labels and threads | Issue has good-first-issue, first-timers, or help-wanted label | preferred |
| Low implementation complexity | Issue body and thread history | Estimated scope appears to be 1-2 days of work for a newcomer; no mention of core system refactoring | preferred |

## Verdict rule

Accept if all seven required checks pass. Reject if any required check fails. Unclear in any required check counts as fail. Preferred checks never change the verdict; they rank accepted issues when multiple candidates pass. If a required check is unclear (evidence genuinely absent), treat as fail.
