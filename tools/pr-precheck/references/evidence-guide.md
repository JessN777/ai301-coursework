# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

- Where it lives: Eval: **Plan context** (in/out scope, files, test plan, deviations) plus the **Candidate PR** unified diff, commit list, and description claims. Live: `plan.md` (including `## Deviations`), `git diff main...HEAD`, and `pr_draft.md`.
- What good looks like: Every changed file is in the plan or a deviation note. Description claims match the hunks. Honest shortfall named in both plan and description is ready (caret-escape without `%VAR%`; image-load path only). Silent extras (new `--time-format`, `truncate()` rewrite, experimental setting) fail. Claiming "docs now document the limitation" when the diff has only a warning is less-than-plan drift.

## Test evidence (harness category: not-tested)

- Where it lives: Eval: **Test evidence** / "Testing" block in the candidate PR, read against the plan's test plan and the issue's repro. Live: `test_evidence.md` and the Testing section of `pr_draft.md`.
- What good looks like: The breaking command is re-run with before and after (or after plus reused unit-2 before). A table of merge-identity cases, a git-parity transcript, or a byte-identical round-trip `diff` counts. Fail "colors work now, cargo test passes" with no paged-output transcript; fail running only the single-file control when the plan's two-file `go build` is the bug; fail a GET casing test when the issue is a POST Content-Type. A short suite mention next to a real repro before/after is not a fail.

## Diff quality (harness category: unreviewable)

- Where it lives: Eval: the candidate **diff** and **commits**. Live: `git diff main...HEAD` and `git log main..HEAD --oneline`.
- What good looks like: The fix is the diff. Fail `DEBUG eprintln` in an accept loop, commented-out first attempts, dead `_unused_buffer_probe` / `count_open_fds` behind `allow(dead_code)`, import TODOs, identical re-printed churn blocks, "wip"/"fmt + cleanup" commits that bury the change.

## Standards and comms (harness category: standards-wall)

- Where it lives: Eval: **Repo facts** (PR template, CONTRIBUTING, AI policy) vs the candidate title/description; **Thread highlights** for maintainer direction. Live: `.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md`, the issue thread, and `pr_draft.md`.
- What good looks like: Template sections have real content (`Closes #N`, type-of-change, testing boxes that match the evidence). Ghostty-style "disclose all AI usage" fails a silent description. Pandas-style required checklist / whatsnew fails when those asks are absent from description and diff. Course Path Review also wants AI-use in Notes for Reviewers even if the template has no labeled disclosure heading. Fidelity of claims vs diff is the plan-fidelity family, not this one.
