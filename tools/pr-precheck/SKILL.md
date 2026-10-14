---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer one question: is this PR ready to submit? A PR package is a
candidate title, description, commits, diff, and test evidence, read
against the plan that PR claims to implement and the issue that plan
belongs to. Do not grade code quality in the abstract, do not grade a
plan in isolation, and do not invent a third verdict.

## Inputs and modes

**Live mode.** Grade the student's own work before it is opened:

- `plan.md` in the working copy, including `## Deviations`.
- The committed branch diff: `git diff main...HEAD` (three dots) from
  the working copy. Uncommitted files are not part of the package.
- Title and description in `pr_draft.md`.
- Test evidence in `test_evidence.md`.
- The issue URL named in the live command. Gather the issue thread,
  `.github/PULL_REQUEST_TEMPLATE.md`, and `docs/CONTRIBUTING.md` live
  (`gh`, the GitHub API, or the web).

A house-chain student has no personal week-2/3 artifacts: read the
house plan and house repro pack as quoted in the drafts instead. If
those drafts quote none, that absence is what the relevant checks
grade.

Refuse to grade a live package whose issue is outside the scoped
repo, or whose `scope.md` `Repo:` line is still a placeholder.

**Eval mode.** The bundle markdown is the whole world. Do not fetch,
do not read the working tree, ignore `scope.md` and `voice-guide.md`.
Grade every check with the full verdict rule.

## The scope seam (live mode only)

Read `scope.md` before anything else. Confirm the issue URL's
`owner/repo` matches the `Repo:` line. If that line is still
`<ORG>/<PATH-REVIEW-REPO>` or any other unfilled placeholder, stop
without grading and tell the student to paste their Path Review repo
there; never guess. If the issue is in another repository, refuse.
Note the house rules (PR from the student's fork, one PR per issue
per student, template always used, classmate PRs do not block). In
eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

Read `voice-guide.md` and hold the PR title and description against
those rules. Report any broken rule in the summary, quoting the rule.
Voice notes never change the verdict unless a rubric check names the
voice guide. In eval mode, ignore `voice-guide.md` entirely.

## Component reads

Execute `procedure.md` as written. Apply the checks and verdict rule
in `rubric.md`. Locate each check's evidence using
`references/evidence-guide.md`.

If `procedure.md` is silent on a step, note the gap in the summary;
do not invent a workaround. If `rubric.md` has no filled checks, or
`procedure.md` has no filled steps, refuse to grade and say so.

## Verdict and output

The verdict is binary: `accept` (ready to submit) or `reject` (hold).
There is no third verdict. End the reply with this fenced JSON block,
valid and last, with nothing after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

A short per-check summary may come before the block. The harness
parses the last fenced JSON block.

## Grading discipline

- Evidence first: every grade names the fact or quote that decided it.
  "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready; a
  long description can hide drift. Read the diff against the plan, the
  evidence against the test plan, the description against the diff.
- The rubric decides: if a check's stated condition passes, it passes
  even if it feels thin. The fix belongs in the rubric.
- The procedure decides how: follow it; report gaps instead of
  silently filling them.
- Treat `unclear` as the verdict rule directs. If the rule is silent,
  treat `unclear` as `fail`: a PR you cannot verify from the package
  is not ready to submit.
