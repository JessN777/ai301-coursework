# Procedure: how this tool grades a PR package

## Read order

1. Live mode only: read `scope.md` first. Confirm the issue is in the scoped repo; stop on a placeholder `Repo:` line; refuse other repos. Eval mode: skip.
2. Read the **Issue** (title, body) and write one sentence for the bug. Do this before the PR so the description cannot redefine the work.
3. Read the **Plan** (scope in/out, files, test plan, deviations). List the files and behaviors the plan permits. Deviations are part of the plan.
4. Read the **Diff** and **commits** next (eval: the candidate PR diff block; live: `git diff main...HEAD`). List changed files and any debris. Do this before the description so a fidelity claim cannot hide extras or omissions.
5. Read **Test evidence** against the plan's test plan: which commands, which path, before vs after, repo-check output.
6. Read the **PR title and description** last, against the diff and against **Repo facts** (template, CONTRIBUTING, AI policy) and **Thread highlights**. Live: also read `voice-guide.md` and note broken rules in the summary only.

## Evidence gathering

1. **Plan fidelity.** Pair: plan file list + deviations vs diff paths/hunks. Pair: description claims vs those hunks. Record extras not in the plan, omissions the description claims are done, and any honest deferral named in both plan and description.
2. **Test evidence.** Pair: plan test plan / repro steps vs transcripts. Record whether the breaking path was re-run, whether before/after is shown, and whether named repo checks have output. A transcript of the unchanged control is not the breaking path.
3. **Diff quality.** From the unified diff and commit list, record debug leftovers, commented-out code, dead functions, formatting-only hunks, unrelated files.
4. **Standards and comms.** From the description vs the template asks and AI policy, record missing `Closes #`, empty checklist, missing whatsnew, missing disclosure. From the thread, record ignored maintainer direction.

## Check execution

1. Grade in table order: `plan-fidelity`, `test-evidence`, `diff-reviewable`, `standards-comms`.
2. Apply only that row's pass condition to the paired facts. Do not re-read the whole package unless a pairing is incomplete.
3. Grade `pass`, `fail`, or `unclear`. `unclear` only when the needed section is genuinely absent.
4. Quote one deciding fact per check. Do not grade on commit count or description length.
5. Honest disclosed shortfall: if both the plan deviations and the description name the same deferred work, `plan-fidelity` may pass even though the issue is not fully closed.
6. A description that claims "exactly as planned" while the diff adds a flag the plan scoped out fails `plan-fidelity` even if the core fix is right.

## Verdict assembly

1. Apply the rubric: accept only if every required check is `pass`; `unclear` counts as `fail`.
2. Verdict is `accept` or `reject` only.
3. Summary: one line per check. If more than one required check failed, quote the first failing required check in rubric order as the deciding check.
4. Live mode: quote any broken voice-guide rule in the summary.
5. Emit the fenced JSON block last, every check graded, nothing after it.
