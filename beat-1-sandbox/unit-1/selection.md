# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/zxcalc/zxlive/issues/555

**Verdict output**

Evaluating: zxcalc/zxlive#555 - Missing several basic rule previews

**Check Results:**
- Maintainer responsive: pass. Last 5 commits are from 2026-08-04, repo is actively maintained with recent collaborator activity
- Repo actively maintained: pass. Human commits within past 6 months; most recent commits are from 2026-08-04
- Repo not archived: pass. Archived field shows false; repo is actively developed
- Issue is bounded: pass. Issue describes specific missing UI features (rule previews); not an umbrella issue
- No active blockers on contribution: pass. No AI policy in contribution guidelines; contributions are welcome
- No current assignee: pass. Issue shows no assignees in repo facts
- No active linked PR: pass. Linked PRs field is empty
- Issue has clear acceptance criteria: pass (preferred). Issue states specific missing features: remove identity, fuse spiders, remove self loops
- Good-first-issue label: pass (preferred). Issue has "good first issue" label
- Low implementation complexity: pass (preferred). Feature is scoped to UI components within a graphics tool

```json
{
  "item": "https://github.com/zxcalc/zxlive/issues/555",
  "checks": [
    {"name": "Maintainer responsive", "grade": "pass", "evidence": "Last commit 2026-08-04 by RazinShaikh, recent merge activity from multiple contributors"},
    {"name": "Repo actively maintained", "grade": "pass", "evidence": "Multiple commits within past 6 months from human contributors"},
    {"name": "Repo not archived", "grade": "pass", "evidence": "archived: no"},
    {"name": "Issue is bounded", "grade": "pass", "evidence": "Issue names specific missing rule previews: remove identity, fuse spiders, remove self loops"},
    {"name": "No active blockers on contribution", "grade": "pass", "evidence": "CONTRIBUTING.md has no AI policy statement; no restrictions found"},
    {"name": "No current assignee", "grade": "pass", "evidence": "assignees: none"},
    {"name": "No active linked PR", "grade": "pass", "evidence": "linked PRs: none"},
    {"name": "Issue has clear acceptance criteria", "grade": "pass", "evidence": "Specifies which rule previews are missing"},
    {"name": "Good-first-issue label", "grade": "pass", "evidence": "Issue carries 'good first issue' label"},
    {"name": "Low implementation complexity", "grade": "pass", "evidence": "Adding UI preview features in a graphics tool is bounded work"}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

Single full run: agreement 20/20 scored items (bar: 18/20: PASS).

The rubric achieved perfect agreement on the first complete run, matching all gold labels across all 20 scored issues and meeting the category floor with at least one match in each composition category (claimed, clear-accept, dead-repo, policy, scope).

**Issue analysis**

issue-11 (zxcalc/zxlive#519): 
- Gold label: accept
- Rubric verdict: accept
- Reasoning: The rubric passed all required checks: maintainer activity confirmed by recent commits (last push 2026-08-04), repo is actively maintained with no archived flag, issue is bounded (performance bug with named causes: "remove inefficient rule application during rewrite"), no assignee or linked PRs, contribution policy passes (no AI bans), and the issue has clear acceptance criteria. The preferred checks also passed: performance bug report with specific description, no good-first-issue label but maintainer-filed status is stronger signal.

**Check rationale**

"Issue is bounded" (required): "Issue describes one specific piece of work; not an umbrella issue, tracking issue, or design discussion without a settled direction"

This check is critical for filtering out work that masquerades as approachable but hides complexity. Umbrella issues masquerade as entry points but actually require coordinating multiple changes, and design discussions without a settled spec waste time on bikeshedding. The rubric requires bounded scope as a gate because a newcomer's first PR should be a clean, reviewable change, not a coordination problem. This check directly addresses Family 3 (scope fits newcomer) from the four families.

**Trade-offs**

The "Issue is bounded" check accepts terse issue bodies when the work itself is bounded. This means the rubric can accept an issue with minimal description if the task is clearly one thing (e.g., a bug report without reproduction steps, but filed by a maintainer and therefore trusted, or a documentation stub with clear scope). This trades polish for realism: many good first issues are filed without extensive ceremony. The trade-off accepts missing some written evidence in favor of judging the actual scope of work. For instance, issue-04 (add rule previews) has minimal description but is clearly bounded: add these specific missing features to the UI. The check passes because the work itself is bounded, not because the issue body is polished.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. **Fit to interests and time**: This issue is a good fit because it involves UI/visualization work in a Python-based graphics library. I have experience with Python and want to improve my skills with graphical tools and proof assistants. The work is scoped to adding missing UI features (rule previews), which I estimate can be completed in 2-3 days including learning the codebase. The repository is small (101 stars) and focused, so onboarding time should be manageable. This issue is in my preferred wheelhouse of bounded, visible-result work rather than refactoring.

2. **What the verdict got right, and what I weighed differently**: The rubric correctly identified this as an active repo with a responsive maintainer, clear scope, and no blockers. The verdict captured the technical signals well. However, I also weighed the fact that the maintainer (RazinShaikh) filed this issue themselves and tagged it good-first-issue, which signals strong confidence in the scope. The rubric doesn't explicitly score "maintainer confidence in scope", but I weighted this heavily because it indicates the work is indeed bounded and that the maintainer stands behind the spec. The rubric's mechanical checks catch the essentials; the human judgment adds confidence.

3. **Anticipated difficulty**: The difficulty is moderate. The main uncertainty is learning the ZX calculus domain and how the proof system works, but this is expected for a first contribution to a specialized library. The difficulty of claiming is low: there are no prior claim comments, no assignee, and it's in a classroom repo where shared issues are normal. I expect a smooth claim process and can proceed immediately to setup and reproduction.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
