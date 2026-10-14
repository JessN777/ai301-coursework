# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | Plan's stated cause (diagnosis / cause sentence) read against the package's Repro evidence block (observed behavior, control runs, expected vs actual) and the Issue body's described bug | The stated cause is consistent with what the repro evidence actually shows. Fail if a control run in the package rules that cause out, if the plan adopts a thread hypothesis the artifacts contradict, or if there is no cause at all. | required |
| scope-bounded | Plan's in-scope / not-in-scope / files-I'll-touch / approach, read against the Issue (what it asked) | The plan is one bounded change that addresses the issue. Fail if it wraps the fix in a redesign, migration, new option/panel/framework, cross-cutting rewrite, or a multi-front campaign the issue did not ask for. Explicit deferral of extra work ("out of scope, later") passes. | required |
| executable | Plan's named files, approach steps, and chosen layer/site of change | A stranger could start without asking the author: at least one real file or code site is named, and one approach is chosen. Fail "poke around", "somewhere", "whichever is easier", or a profile-and-optimize with no files. | required |
| test-plan-decisive | Plan's test plan read against the Repro evidence steps and artifacts | The test names an observable after-fix outcome a stranger could check (specific output, exit code, color, parsed value), preferably by re-running the repro. Fail "should feel fast", "nothing else should feel broken", or "run the full test suite" with no observable for this fix. | required |
| thread-conventions | Candidate plan comment read against Thread highlights (maintainer direction, isolated files, "please test this patch") and Repo facts contribution / AI policy | If a maintainer in the thread already isolated a file, posted a patch, or asked for a specific test, the comment engages that direction rather than substituting an unrelated workaround. If the repo-facts policy requires disclosing AI usage in issues or comments, the plan comment discloses it (eval packages are AI-assisted work). If the policy only requires human-written comments, pass when the comment is specific and human-voiced. If there is no AI-disclosure mandate and no ignored maintainer direction, this check passes. | required |

## Verdict rule

Accept only if every required check is `pass`. Preferred checks never change the verdict. Treat `unclear` (`?`) on a required check as `fail`: a plan you cannot verify from the package is not ready to build from.
