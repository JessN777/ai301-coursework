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
**Pull Request:** https://github.com/andre-motta/tongs/pull/464

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

**Unit 7: The ship-gate passed the README branch after two stops**

I installed the ship-gate on the tongs clone and wrote ship-manifest.md with the control-character check and the markdown lint from the docs CI job. The first real run stopped because Windows cmd.exe could not execute the extensionless Unix lint path. I changed that row to markdownlint-cli2.cmd. The next run stopped because test_evidence.md, a local file the lint glob still sees, had a bare URL and unlabeled fences. I fixed those lines. The third run passed: both repo checks ok, and pr-precheck accepted plan-fidelity, test-evidence, diff-reviewable, and standards-comms. I opened https://github.com/andre-motta/tongs/pull/464 from the fork after that pass. pytest, ruff, the site build, and desktop lint stay excluded, with the reason and date in the manifest.

**Unit 8: The PR-monitor read a quiet pull request and drafted a wait note I did not send**

I wrote a playbook with a 7-day first-review threshold, one nudge maximum, and a 30-day walk-away, then ran the PR-monitor from the tongs clone on fix/318-readme-keybindings. The first full run refused because it still saw the empty template (I had started it in the same moment I saved the playbook). After the file was filled, the run at 2026-10-19T04:18:04Z read pull request 464 as QUIET: opened 2026-10-19T02:59:18Z, zero comments and reviews, mergeable, merge state UNSTABLE, no checks reported. It drafted "No nudge yet. Wait note." I did not post it. The threshold is not met until 2026-10-26T02:59Z.

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

Part 2 is a documentation mismatch, not a behavior bug. The README Keybindings section was written as if `o` were global, as if the desktop app had no keys of its own, and as if the diff viewer and Pipeline Escape handling matched an older table. docs/reference/keybindings.md is the page the issue treats as the source of truth. The line numbers it cites in src/tongs/widgets/diff_panel.py are a banner string in this clone, so I did not edit that file.

**Proposed Solution**

Edit README.md only, for the four named disagreements. Do not change part 3 (the check lists), and do not change Python or desktop code.

**Implementation Plan**

1. Point the desktop sentence at the reference's desktop section.
2. Move `o` from the Global table to the Inbox table, and note under MR detail that it opens the current MR and is not bound on the repository list.
3. Add `e` and `F` to the Diff viewer table, worded like the reference.
4. Replace the two Pipeline Escape rows with one row matching the reference.

Deviation, recorded before the pull request: the reference intro says the main-screen keys also apply on the repository list, but the `o` cell and the issue both say `o` is inbox and MR detail. The README follows the issue and the cell.

**Toolkit**

- Tool: the plan file the ship-gate's pr-precheck read (plan.md in the clone, not committed)
- What it produced: a pass on plan-fidelity for README.md only
- Difficulties: the issue's diff_panel.py line numbers do not match this clone
- What changed: the plan says the README follows the reference text, not those line numbers

---

## Testing Strategy

The observable is the four README disagreements, checked against docs/reference/keybindings.md before the edit (the issue comment) and after it (the diff). The repo checks I actually ran are `python scripts/check_control_chars.py` (738 text files, no disallowed characters) and the markdownlint command from issue #318 (0 issues). pytest, ruff, and the site build were not run. The manifest records that exclusion, and the pull request says the same thing.

**Toolkit**

- Tool: ship-gate, running the manifest commands and then pr-precheck on test_evidence.md
- What it produced: a pass on test-evidence after the local evidence file itself was lint-clean
- Difficulties: the first lint failure was test_evidence.md, not README.md
- What changed: labeled the fences and removed the bare URL in that local file

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**2026-10-18**

Claimed tongs #318 part 2 only, after the voice-guard passed the draft. Compared README.md with docs/reference/keybindings.md on a shallow clone and posted that comparison. Did not start the app.

**2026-10-18**

Built the README edit on fix/318-readme-keybindings (commit 9ef99be). The ship-gate blocked twice, once on the Windows lint path and once on test_evidence.md, then passed. Opened https://github.com/andre-motta/tongs/pull/464 from the fork. Did not take part 3.

**2026-10-18**

Ran the PR-monitor against pull request 464. State was quiet, under a day, with no comments. The draft said to wait. I did not post a nudge.

**2026-10-19**

andre-motta approved and merged pull request 464 at 2026-10-20T00:37:02Z. He said the four mismatches now match the keybinding reference, and that the note about where `o` is bound was useful. He reworded the description because GitHub treats "close #318" as a closing keyword even after "does not", so #318 stays open for part 3. I did not take part 3.

**Toolkit**

- Tool: ship-gate
- What it produced: two stops, then a pass, then the pull request
- Difficulties: Windows could not run the Unix lint path, and a local notes file failed the same lint
- What changed: the manifest command and the local evidence file, then a fresh gate run before the pull request opened

---

## Pull Request

**PR Link:** https://github.com/andre-motta/tongs/pull/464

**PR Description:** Part 2 of #318 only. The four named README disagreements now match the reference. The description explains each unchecked checklist box and discloses that Cursor Grok 4.7 drafted the edit. andre-motta later reworded the sentence about #318 so GitHub would not treat it as a closing keyword.

**Maintainer Feedback:**

- 2026-10-18: none yet
- 2026-10-18, monitor run 21:18 local: still none. Zero comments and reviews. I did not send a nudge.
- 2026-10-19: andre-motta approved and merged. He confirmed the four mismatches match the reference, noted the `o` binding sentence, and kept #318 open for part 3. https://github.com/andre-motta/tongs/pull/464#pullrequestreview-5579428498

**Status:** Merged on 2026-10-19 by andre-motta. Part 3 of #318 is still open. I did not take it.

**Toolkit**

- Tool: ship-gate on fix/318-readme-keybindings, then gh pr create from the fork
- What it produced: a pass, then pull request 464
- Difficulties: the Unix lint path failed in Windows cmd, and a local notes file failed markdownlint
- What changed: the manifest command uses markdownlint-cli2.cmd, and the local evidence file was lint-clean before the passing run

---

## Learnings and Reflections

**Technical Skills Gained**

I learned how tongs wants a docs change checked: `scripts/check_control_chars.py`, then markdownlint-cli2 from `.github/linters`, then a signed-off commit with a Co-authored-by line. I also learned that README key tables and `docs/reference/keybindings.md` disagree in specific cells, and that the `o` binding belongs on Inbox and MR detail, not the repo list.

**Challenges Overcome**

The scout's first search only returned issues opened that day, so I added a created-before date and one hit per repository before I trusted an accept. The voice-guard stopped until `claude.exe` was on PATH. The ship-gate stopped twice, first because Windows cmd could not run the Unix lint path, then because a local notes file failed the same lint. The PR-monitor's first full run refused an empty playbook. Each stop changed the command, the file, or the playbook before the next run.

**What I'd Do Differently Next Time**

I would fill the playbook and confirm the file on disk before starting the monitor, so the first full run is the real one. I would also run markdownlint on local `*.md` notes before treating a lint failure as a problem in the change.

---

## Resources Used

- https://github.com/andre-motta/tongs/issues/318, the issue, including the named files for part 2 and the instruction not to take part 3 in the same pass
- https://github.com/andre-motta/tongs/blob/main/docs/reference/keybindings.md, the reference the README tables were aligned to
- https://github.com/andre-motta/tongs/blob/main/CONTRIBUTING.md, for the signed-off commit, the Co-authored-by line, and the checklist the pull request body accounts for
- The docs CI job in the tongs repo, which named `scripts/check_control_chars.py` and the markdownlint-cli2 install the ship-manifest runs
