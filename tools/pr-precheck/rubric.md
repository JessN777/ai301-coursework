# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-fidelity | Diff file list and hunks read against the plan's in-scope / not-in-scope / files / approach and any `## Deviations`; PR description claims ("exactly as planned", "docs now updated", "no functional extras") read against the same diff | Every changed file and behavior is inside the plan plus named deviations, and the description does not claim work the diff omits or omit extras the diff adds. An honestly disclosed shortfall (plan and description both name what was deferred) passes. Fail silent extras (new flags, rewrites, config, extra files), silent omissions, or a fidelity claim the diff contradicts. | required |
| test-evidence | Test-evidence section (before/after transcripts, named commands) read against the plan's test plan and the issue/repro steps | The evidence shows the plan's primary observable on the path that actually breaks: a before and after (or after plus an explicit reuse of a prior before). Fail "tested locally" / "tests pass" / "verified on my machine" with no command output, evidence of only an unchanged control path, or skipping the plan's named breaking repro entirely. Showing the repro before/after is enough even if a suite log is short. An honest "this check produced X; here is why" still counts. | required |
| diff-reviewable | Unified diff and commit subjects | The planned change is visible. Fail leftover debug prints (`eprintln`, `console.log` used for debugging), commented-out attempts, dead helpers behind `allow(dead_code)`, TODO-on-import debris, formatting-only churn hunks, or unrelated drive-by edits folded into "wip"/"fmt + cleanup" commits. | required |
| standards-comms | PR title/description against Repo facts PR template / CONTRIBUTING / AI policy, plus Thread highlights for maintainer direction | Required template sections are filled with real content (including `Closes #N` / checklist / whatsnew when the template asks). If policy requires disclosing AI usage, the description discloses it (eval packages are AI-assisted). If a maintainer isolated a file or asked a specific test, the description engages that. Fail a visibly ignored checklist or a silent AI-policy wall. | required |

## Verdict rule

Accept only if every required check is `pass`. Preferred checks never change the verdict. Treat `unclear` on a required check as `fail`: a PR you cannot verify from the package is not ready to submit.
