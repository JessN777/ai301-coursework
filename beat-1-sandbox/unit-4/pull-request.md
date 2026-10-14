# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/236

**Branch**

docs/73-openrouter-env-example

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. First full run (`--skill ~/.claude/skills/pr-precheck --save-run eval-run.txt`): **14/20**, categories `clear-accept 1/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3`. All six misses were gold-accept packages failed on `test-evidence` (pkg-05, pkg-08, pkg-11, pkg-13, pkg-16, pkg-19).
2. After loosening `test-evidence` so a repro before/after is enough even if the suite log is short: `--only pkg-05,pkg-08,pkg-11,pkg-13,pkg-16,pkg-19,pkg-04,pkg-07` (not-tested canaries pkg-04 and pkg-07). Partial result **8/8**; canaries stayed reject.
3. Confirming full run (harness-written `beat-1-sandbox/unit-4/eval-run.txt`, 2026-10-14T06:40:42Z): **20/20 scored items, bar PASS**, categories `clear-accept 7/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3`. That agreement line matches the committed `eval-run.txt`.

**Package analysis**

pkg-20 (ghostty-org/ghostty#13604), category `standards-wall`. Gold label: **reject**. Rubric verdict: **reject**.

The diff is a bounded mode-2031 fix with decisive evidence. Gold holds it because ghostty requires disclosing all AI usage and the description does not (eval packages are AI-assisted). My `standards-comms` check fails a missing disclosure when the repo-facts policy requires it, so the package is reject even though plan-fidelity, test-evidence, and diff-reviewable would pass. That is the 2-item floor a rubric with no template/disclosure check cannot see.

**Check rationale**

`test-evidence` (required), quoted from the uploaded `tools/pr-precheck/rubric.md`:

> The evidence shows the plan's primary observable on the path that actually breaks: a before and after (or after plus an explicit reuse of a prior before). Fail "tested locally" / "tests pass" / "verified on my machine" with no command output, evidence of only an unchanged control path, or skipping the plan's named breaking repro entirely. Showing the repro before/after is enough even if a suite log is short. An honest "this check produced X; here is why" still counts.

The first wording also demanded visible output for every claimed repo-check (`make test-unit`, `cargo test`, …). That failed every clear-accept except pkg-02, because those PRs show the repro table and a short suite mention, not a full log. I dropped the suite-log demand and kept the breaking-path rule, then re-ran not-tested canaries so pkg-04 and pkg-07 could not flip to accept.

**Trade-offs**

The loosened check still holds "tests pass" with no transcript (pkg-04, pkg-10) and evidence of the unchanged path only (pkg-07, pkg-14). What it gives up: a PR that shows the repro before/after but never ran `yarn test` when the plan named it can now pass. I accepted that after the canary `--only` kept pkg-04/pkg-07 as reject, because requiring a full suite paste was failing the clear-accept floor.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
