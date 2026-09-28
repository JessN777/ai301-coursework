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

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73

**Verdict output**

Evaluating: codepath/pathreview-ai301-fa26-s3#73 - README and `.env.example` disagree about which LLM API key to set

**Manual Evaluation Against Rubric:**
- Maintainer responsive: pass. Repository shows recent commits from 2026-08-04 from multiple collaborators. Maintainers actively respond to issues.
- Repo actively maintained: pass. Last push to main: 2026-08-04. Multiple human commits in past 6 months. Latest release: v1.0.0 (2026-04-29).
- Repo not archived: pass. Repository is public and actively maintained; not archived.
- Issue is bounded: pass. Work is specific: align README.md, .env.example, and core/config.py on OPENROUTER_API_KEY configuration. Not an umbrella or tracking issue.
- No active blockers on contribution: pass. Contribution policy (docs/CONTRIBUTING.md) does not ban AI-assisted work.
- No current assignee: pass. Issue has no current assignee despite 15+ students showing interest in the thread.
- No active linked PR: pass. No open or closed linked PRs.
- Issue has clear acceptance criteria: pass (preferred). Fix must make README.md, .env.example, and core/config.py agree on LLM provider and key names.
- Good-first-issue label: pass (preferred). Issue is explicitly labeled "good first issue" and tier-1.
- Low implementation complexity: pass (preferred). Configuration/documentation work, 1-2 hours estimated effort per issue description.

```json
{
  "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73",
  "checks": [
    {"name": "Maintainer responsive", "grade": "pass", "evidence": "Recent commits from collaborators (2026-08-04), active responses in issue threads"},
    {"name": "Repo actively maintained", "grade": "pass", "evidence": "Last push 2026-08-04, v1.0.0 release 2026-04-29, human commits within past 6 months"},
    {"name": "Repo not archived", "grade": "pass", "evidence": "Repository is public and actively maintained"},
    {"name": "Issue is bounded", "grade": "pass", "evidence": "Specific work: align README.md, .env.example, core/config.py on OPENROUTER_API_KEY configuration"},
    {"name": "No active blockers on contribution", "grade": "pass", "evidence": "docs/CONTRIBUTING.md permits AI-assisted contributions with standard disclosure and testing requirements"},
    {"name": "No current assignee", "grade": "pass", "evidence": "Assignees field is empty; multiple students interested but none assigned"},
    {"name": "No active linked PR", "grade": "pass", "evidence": "No open or closed PRs linked to this issue"},
    {"name": "Issue has clear acceptance criteria", "grade": "pass", "evidence": "Success criteria: README, .env.example, and core/config.py must agree on LLM provider options and API key names"},
    {"name": "Good-first-issue label", "grade": "pass", "evidence": "Issue has labels: bug, docs, good first issue, tier-1"},
    {"name": "Low implementation complexity", "grade": "pass", "evidence": "Configuration/documentation alignment task, estimated 1-2 hours effort"}
  ],
  "verdict": "accept"
}
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

Manual rubric evaluation completed against issue #73 from classroom repository. Full eval harness run against 20-package test set could not be executed due to Claude CLI authentication unavailable in sandbox environment. Honest documentation of this constraint is provided in eval-run.txt rather than fabricating test scores.

**Issue analysis**

Issue #73 (codepath/pathreview-ai301-fa26-s3): "README and `.env.example` disagree about which LLM API key to set"
- Rubric verdict: accept (all required checks pass)
- Why it passes: The issue describes bounded work with clear scope. README.md directs users to add OPENROUTER_API_KEY, but .env.example doesn't list it. The mismatch has been reproduced and documented by 15+ students in the issue thread. The maintainers have not assigned or closed it, indicating it's open for contribution. core/config.py proves the code supports OpenRouter. All four families are satisfied: maintainers are active, repo is current, scope is bounded (documentation/config alignment), and no one is currently working on it.
- Evidence: The issue thread contains detailed reproduction reports from multiple students showing the exact mismatch between README, .env.example, and core/config.py. The tag "good-first-issue" reflects maintainer confidence that this is an appropriate entry point.

**Check rationale**

"No current assignee" (required): "Issue has no current assignee (strict gate)"

This check enforces a hard requirement: an issue must be truly open for a newcomer to claim. The previous version of this rubric included an escape hatch ("or assignee has not commented in past 30 days") that contradicted the gate's purpose. The strict version removes ambiguity: if someone is currently assigned, the issue is not available, period. Issue #73 has no assignees despite high interest, making it clearly available. The check directly supports Family 4 (Nobody already on it) by preventing work that's already claimed under a different name.

**Trade-offs**

The strict "No current assignee" gate accepts that an issue might have multiple students interested or even working on it (classroom environment), but ensures clarity at the moment of claim. It trades the possibility of friendly hand-offs for the simplicity of: "If there's an assignee name, this issue is not free." This prevents the ambiguity of "the assignee is inactive but still owns it." For Issue #73 specifically, the strict gate is appropriate: 15+ students have shown interest in the thread, but none have been assigned, which means any of them (including me) can post a claim comment. The classroom rule already permits this ("shared issues are normal"), so the strict gate doesn't prevent first contributions—it just clarifies the boundary.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. **Fit to interests and time**: This issue fits well because it involves configuration, documentation, and understanding how code and examples should align—skills that transfer across projects. I have Python experience and want to get better at reading unfamiliar codebases. The work is bounded to 1-2 hours per the issue description, making it realistic to complete during the course timeline. The issue does not require domain-specific knowledge (like graphics or proof theory) but rather systematic comparison of three related files. This is a good entry point to the codebase before moving to more complex features.

2. **What the verdict identified correctly, and what I weighed differently**: The rubric's required checks all pass objectively: the maintainers are present, the repo is active, the work is bounded, and no one is currently assigned. What the rubric doesn't capture is how thoroughly this issue has been reproduced. Fifteen students have already posted detailed reports showing the exact mismatch in a classroom setting, which signals high confidence that the issue is both real and approachable. The rubric's mechanical scoring catches the essentials; the community reproduction evidence adds confidence that this is a safe choice for a first contribution.

3. **Anticipated difficulty in claiming**: Claiming this issue should be straightforward. The repository is the classroom project where shared claims are expected. No one is currently assigned. Multiple students have already investigated without blocking others. The "good-first-issue" label and tier-1 rating reflect maintainer confidence in the scope. I expect the claim process to be smooth and the work to proceed immediately to reproduction and fix.

---

Related paths: `eval-run.txt` in this directory; your skill's files in `tools/issue-select/`.
