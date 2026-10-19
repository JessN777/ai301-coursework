# Contribution: tongs #318 part 2, README key tables vs the keybinding reference

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Jessica Le Nguyen
**GitHub Username:** JessN777
**Issue:** https://github.com/andre-motta/tongs/issues/318
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built the issue scout and corrected a search that only saw brand-new issues**

I installed issue-scout, kept the unit 1 rubric and evidence guide, and wrote a fit profile plus two good-first-issue queries for Python and JavaScript. GitHub CLI was not logged in, and the first search's hundred hits were issues opened on October 18 or 19, with one repository occupying the top of the list. I bounded the queries to issues created before October 5, kept one hit per repository, and patched the maintainer-responsive check so silence on a maintainer-opened issue is not a failed reply. Graded under that patch, tongs #318, agent-sweep #207, and pydynox #490 passed, and vogt-fixture #8 and vibey #1292 failed because each already has an open pull request.

**Unit 6: Installed the voice-guard and wrote repo memory for tongs**

I installed the voice-guard, extended the voice guide with claim, question, and ping rules, and swapped repro-check and plan-check onto the wild scopes. The first two manual checks stopped because `claude.exe` was not on PATH; after I added its directory, the claim draft passed, and a body-less `gh issue comment --help` was stopped on purpose. I posted the claim and a file-comparison note on tongs #318. `CLAUDE.local.md` is under 60 lines, distilled from CONTRIBUTING.md and the keybinding files, and `git status` in the clone does not show it because `.git/info/exclude` hides it. I also replaced the rubric's "Issue is bounded" gate with "scope-feasible", because #318 is one docs task spread across several named files.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I searched open Python and JavaScript issues labeled good first issue. The first page was all issues created on October 18 or 19, so I bounded the queries to issues created before October 5 and kept one hit per repository. The scout accepted three: tongs #318, agent-sweep #207, and pydynox #490. It rejected vogt-fixture #8 and vibey #1292 because each already had an open pull request. I chose tongs #318, part 2 only. The verdict was accept, and the work is a documentation comparison, which is the kind of bounded Python-project task in my fit profile. I want to learn how a real repo wants docs and CI checks described, without taking part 3 in the same pass.

The scout's first ranking was not trustworthy: fewest-comments-first promoted brand-new issues and let one repo fill the list. The old maintainer-responsive check would also have rejected tongs #318 for an empty thread even though andre-motta was merging pull requests that day. I changed the queries, the one-per-repo rule, and that check before I trusted the accept. Claim comment: https://github.com/andre-motta/tongs/issues/318#issuecomment-6258495890

**Toolkit**

- Tool: issue-scout, using the Python and JavaScript good-first-issue queries and the patched rubric
- What it produced: an accept on tongs #318, with the other two accepts and the two open-PR rejects recorded in scan-output.md
- Difficulties: the unbounded query only returned issues opened on October 18 or 19, and the old maintainer-responsive check treated a silent maintainer-opened thread as a failure
- What changed: a created-before date, one issue per repository, and a maintainer-responsive pass condition that fails only when a contributor comment has waited more than 30 days

---

## Understanding the Issue

**Problem Description**

Part 2 of tongs #318: the README keybinding tables do not match docs/reference/keybindings.md. I am not taking part 3 (the CI check lists) in this pass.

**Expected Behavior**

The README tables should list the same keys, with the same meaning, as the keybinding reference. The desktop sentence should point at the reference's desktop section instead of saying the desktop app only uses labelled controls.

**Current Behavior**

On a fresh clone, without starting the app: README.md line 273 still says the desktop workspace uses labelled controls, while the reference has a Desktop app (beta) key table. The README Global table still lists `o`. src/tongs/views/repo_list.py does not bind `o`. The README Diff viewer table has no `e` or `F` row; the reference has `e` and Shift+F. The README Pipeline tab has two Escape rows; the reference has one.

**Affected Components**

README.md Keybindings section, docs/reference/keybindings.md, and the binding lists the issue points at in src/tongs/views/repo_list.py and src/tongs/widgets/diff_panel.py. The line numbers the issue cites in diff_panel.py are a banner string in this clone, not the bindings.

**Toolkit**

- Tool: the file comparison in the fresh clone, checked against the voice guide before I posted it
- What it produced: the comparison comment at https://github.com/andre-motta/tongs/issues/318#issuecomment-6258522610
- Difficulties: the issue's diff_panel.py line numbers do not match this clone
- What changed: I reported that mismatch instead of treating those lines as the key bindings

---

## Reproduction Process

**Environment Setup**

Windows 11, a shallow clone of andre-motta/tongs at the default branch. I did not create a virtualenv or start the app. Part 2 is a file comparison.

**Steps to Reproduce**

1. Clone andre-motta/tongs.
2. Read README.md from the Keybindings heading through the Pipeline tab.
3. Read the matching sections in docs/reference/keybindings.md, plus BINDINGS in src/tongs/views/repo_list.py.
4. Observed result: the four disagreements in part 2 are still in the files. The cited diff_panel.py lines are not the key bindings.

**Reproduction Evidence**

- **Commit showing reproduction:** not in a fork yet. The comparison is the comment on the upstream issue.
- **Screenshots/logs:** https://github.com/andre-motta/tongs/issues/318#issuecomment-6258522610
- **My findings:** README and the reference still disagree on the desktop sentence, global `o`, diff `e` / Shift+F, and the Pipeline Escape rows. I have not found the `e` and `F` bindings at the line numbers the issue names.

**Toolkit**

- Tool: repro-check's wild scope, plus the voice-guard on the comparison comment
- What it produced: a posted file comparison, not an "I reproduced the running app" claim
- Difficulties: none in the file read. The app was not part of the check.
- What changed: nothing in the repro steps. The scope file is now the wild scope, so a stranger's claim would have blocked me.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**2026-10-18**

Claimed tongs #318 part 2 only, after the voice-guard passed the draft. Compared README.md with docs/reference/keybindings.md on a shallow clone and posted that comparison. Did not start the app. Did not take part 3.

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
