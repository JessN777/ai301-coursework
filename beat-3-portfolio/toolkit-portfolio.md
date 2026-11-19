**Student:** Jessica Le Nguyen

## Featured Tools

I featured the four tools I used on the tongs contribution, because each one changed after a real run failed or came back empty. issue-scout picked the issue. voice-guard checked the words I posted. ship-gate decided whether the branch could open a pull request. pr-monitor decided whether a quiet thread was a reason to nudge.

**issue-scout**

**What it is, and the judgment hole I wrote:** It searches open GitHub issues and grades them against a rubric I can patch. The judgment I wrote is the fit profile, the two good-first-issue queries, and the rubric gates for scope and maintainer response.

**How it evolved, dated:** On October 18, 2026 the first search returned a hundred issues, almost all opened that day or the next, with one repository filling the top of the list. I bounded the queries to issues created before October 5 and kept one hit per repository. The same day I replaced the rubric gate "Issue is bounded" with "scope-feasible", and I changed maintainer-responsive so a silent maintainer-opened issue is not a failed reply. It fails only when a contributor comment has waited more than 30 days.

**Evidence:** After that change the scout accepted tongs #318, agent-sweep #207, and pydynox #490, and rejected vogt-fixture #8 and vibey #1292 because each already had an open pull request. I claimed tongs #318, part 2 only: https://github.com/andre-motta/tongs/issues/318#issuecomment-6258495890

**voice-guard**

**What it is, and the judgment hole I wrote:** It holds an outgoing GitHub comment or pull request body against my voice guide before anything posts. The judgment I wrote is that guide: claim the part I will look at, do not promise a fix, and do not say I reproduced a bug before I ran anything.

**How it evolved, dated:** On October 18, 2026 the first two manual checks stopped because `claude.exe` was not on PATH. I added its directory and ran the claim draft again. I also pointed the hook at a body-less `gh issue comment --help` on purpose, to confirm a comment with no body cannot pass.

**Evidence:** The claim draft passed after the PATH fix, and the body-less command was stopped. The comment that then posted is the tongs #318 claim linked above. The comparison comment, posted only after the same guard, is https://github.com/andre-motta/tongs/issues/318#issuecomment-6258522610

**ship-gate**

**What it is, and the judgment hole I wrote:** It runs the commands in my ship manifest, then my own pr-precheck, before a pull request opens. The judgment I wrote is `ship-manifest.md`: which repo checks must pass, and which ones are excluded with a date and a reason.

**How it evolved, dated:** On October 18, 2026 the first real run on `fix/318-readme-keybindings` stopped because Windows cmd.exe could not execute the extensionless Unix lint path. I changed that row to `markdownlint-cli2.cmd`. The next run stopped because local `test_evidence.md` had a bare URL and unlabeled fences. I fixed those lines. On October 20 a later run against a stale local `main` treated the already-merged README commit as part of the new branch. I reran with `--base upstream/main`. The same day pr-precheck marked standards-comms unclear because the description named Cursor Grok 4.7 while the grader was another model. I patched that check so a disclosure passes when it names the tool on the commit trailer.

**Evidence:** The third October 18 run passed, including `No disallowed control characters in 738 text file(s).` and Markdown lint with zero issues. Pull request 464 opened only after that pass: https://github.com/andre-motta/tongs/pull/464. The Windows command the manifest kept is `.github\linters\node_modules\.bin\markdownlint-cli2.cmd`.

**pr-monitor**

**What it is, and the judgment hole I wrote:** It reads a pull request and drafts the next move from my playbook. It does not post. The judgment I wrote is the playbook: a 7-day first-review threshold, one nudge, no @ mentions, and a 30-day walk-away.

**How it evolved, dated:** On October 18, 2026 the first full run refused because the playbook file was still the empty template. I had started the run in the same moment I saved the rules. After the four sections were filled, I ran it again.

**Evidence:** The filled run at 2026-10-19T04:18:04Z read pull request 464 as quiet, under a day, with zero comments. It drafted "No nudge yet. Wait note." I did not post it. The threshold was 2026-10-26T02:59Z. andre-motta merged 464 on October 19, before any nudge.

## Inventory

- issue-select: the unit 1 issue grader in `tools/issue-select`. It grades a sandbox bundle against a written rubric. The live search that chose tongs #318 was issue-scout, not this copy.
- repro-check: grades a reproduction package. On the tongs issue I used its wild scope, and the posted comparison says I did not start the app.
- plan-check: grades a plan against the issue. The October 14 eval run scored 20/20. The live plan for the README edit stayed in the tongs clone and was read by the ship-gate.
- pr-precheck: grades a pull request package. The October 14 eval run scored 20/20. Live, the ship-gate calls it after the manifest commands, which is how the README branch and the later check-list branch were judged.

## The Arc

**Beat 1**
Date: October 18, 2026
Friction: The unbounded issue search returned issues opened that day, so fewest-comments-first was ranking brand-new tickets.
Change: I added a created-before date, one issue per repository, and a maintainer-responsive rule that fails only after a contributor has waited more than 30 days.
Result: tongs #318 passed, I claimed part 2, and that claim is the issue comment linked above.

**Beat 2**
Date: October 18, 2026
Friction: The voice-guard stopped the claim draft because `claude.exe` was not on PATH.
Change: I put the Claude directory on PATH and reran the draft. I also confirmed a body-less comment command is stopped.
Result: The claim and the file-comparison note both posted on tongs #318.

**Beat 3**
Date: October 18, 2026
Friction: The ship-gate stopped twice, first on the Unix lint path under Windows cmd, then on bare URLs and unlabeled fences in `test_evidence.md`.
Change: The manifest command became `markdownlint-cli2.cmd`, and the local evidence file was made lint-clean before the next run.
Result: The third run passed, and pull request 464 opened from the fork. andre-motta merged it on October 19.

**Beat 4**
Date: October 18, 2026
Friction: The PR-monitor refused to draft because the playbook was still empty, and a same-evening quiet thread was easy to mistake for a stall.
Change: I filled the 7-day threshold, one-nudge rule, and 30-day walk-away, then ran the monitor again.
Result: It drafted a wait note. I did not send a nudge. The maintainer merged pull request 464 the next day.

**Beat 5**
Date: October 20, 2026
Friction: A ship-gate run of the check-list branch used stale local `main`, so the diff looked like it still contained the already-merged README edit. A later run then held the pull request because the AI disclosure named Cursor Grok 4.7 and the grader was a different model.
Change: I set the base to `upstream/main`, and I patched standards-comms so the disclosure is checked against the commit trailer rather than against the grader's model.
Result: The gate passed, pull request 465 opened, and andre-motta merged it the same night, which closed issue 318.

## Limitations and What's Next

The toolkit can stop a bad search, a careless comment, an unready branch, and a premature nudge. It cannot tell me whether a documented key actually fires in the running app, and it cannot see a pull request that was opened by walking around the gate. Next I would make the ship-gate base explicit in the manifest, so a stale local `main` cannot inflate the diff, and I would run Markdown lint on local notes before treating a lint failure as a problem in the change.

**Tool limits.**

issue-scout: A created-before date hides a good issue opened after the cutoff, and the fit profile never changes an accept or reject.
voice-guard: It only checks commands it can read. A post made with a raw API call, or with `claude` missing from PATH, never gets a voice verdict.
ship-gate: It grades the branch against whatever base the command names. A stale local main, and a Windows checkout that stores a docs symlink as a plain file, both made a docs build look finished when the site had not really been checked.
pr-monitor: It will not draft from an empty playbook, and a wait note is only as good as the threshold I wrote. It does not notice a maintainer merging a different part of the same issue.
