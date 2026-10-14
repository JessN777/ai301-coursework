# Procedure: how this skill grades a plan package

## Read order

1. In live mode only, read `scope.md` first. Confirm the issue URL's `owner/repo` matches the `Repo:` line. If the line is still a placeholder, stop without grading. If the issue is outside that repo, refuse. Note the house rules (classmate plans do not block; no piggyback; branch on the fork). In eval mode, skip this step.
2. Read the **Issue** (title, body, what "done" would change) and write down the symptom in one sentence. Do this before the plan so the plan cannot define the bug.
3. Read **Repro evidence** next: environment, steps, observed, expected, and any control run. Note the behavior those artifacts pin down, and which causes they already rule out. Checks later must follow this, not the plan's story.
4. Read **Thread highlights** and **Repo facts** (templates, contribution policy, AI policy). Note any maintainer direction (isolated file, posted patch, requested test) and whether disclosure is required.
5. Read the **Candidate plan** (diagnosis, scope, files, approach, test plan, risks/unknowns, deviations if present).
6. Read the **Candidate plan comment** last, the way a maintainer on the thread would. In live mode, also read `voice-guide.md` and note broken rules in the summary only.

## Evidence gathering

1. **Diagnosis and grounding.** From the plan, copy the cause sentence. From Repro evidence, copy the observed behavior and every control run. Record whether the cause cites those artifacts or contradicts them.
2. **Scope.** From the plan, copy in-scope, not-in-scope, and the file list. From the Issue, copy what was asked. Record extra campaigns (migrations, rewrites, new options) that are not deferred.
3. **Executability.** From the plan's files and approach, record named paths and whether one site of change is chosen. If the approach is a menu of unchosen options, record that.
4. **Test plan.** From the plan's test section, record the after-fix observable. From Repro evidence, record the steps it maps onto. If the test is only "full suite" or a feeling, record that there is no observable.
5. **Honesty.** From risks/unknowns/deviations, record stated uncertainty vs claims of certainty the evidence does not support. (No required check keys off this family unless a diagnosis check already failed.)
6. **Comms.** From the plan comment, record whether it engages thread direction and whether it discloses AI use when Repo facts require it. Live: gather the live thread and CONTRIBUTING/AI policy from the locations in the evidence guide.

## Check execution

1. Grade checks in table order: `diagnosis-grounded`, `scope-bounded`, `executable`, `test-plan-decisive`, `thread-conventions`.
2. For each check, apply only that row's pass condition to the facts gathered for it. Do not re-read the whole package unless the gathered facts are insufficient.
3. Grade `pass`, `fail`, or `unclear`. `unclear` is only for genuinely missing evidence (the section is absent), not for "I am unsure."
4. Quote one deciding fact in the check's `evidence` field. Do not grade on heading count, length, or polish.
5. If a control run rules the diagnosis out, `diagnosis-grounded` is `fail` even if the rest of the plan is polished.
6. If extra work is explicitly out of scope, `scope-bounded` may `pass`. If extra work is in the approach as something this change will do, `fail`.

## Verdict assembly

1. Apply the rubric verdict rule: accept only if every required check is `pass`; treat `unclear` as `fail`; preferred checks (none in this rubric) never change the verdict.
2. Set `verdict` to `accept` or `reject`. There is no third verdict.
3. In the summary, one line per check. Quote the deciding fact for any `fail`. In live mode, quote any broken voice-guide rule.
4. Emit the fenced JSON block last, with every check graded, then nothing after it.
