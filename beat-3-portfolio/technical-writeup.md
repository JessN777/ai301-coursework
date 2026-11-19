# Making the tongs docs agree with the app and with CI

## Overview

tongs is an open source tool for reading merge requests in the terminal and in a desktop app. [Issue #318](https://github.com/andre-motta/tongs/issues/318) said three sets of pages had drifted: a homepage key, the README shortcut tables, and the lists of checks a contributor is told to run. Part 1 was already done. I took part 2 first, a README-only correction, and opened [pull request #464](https://github.com/andre-motta/tongs/pull/464) after a local check stopped me twice. The maintainer merged it on October 19, 2026, and rewrote one sentence so the issue would stay open. I then did part 3, the check lists, in [pull request #465](https://github.com/andre-motta/tongs/pull/465). He merged that the next night, and the issue closed.

## What happened

I did not start from the tongs issue. On October 18 I searched open Python and JavaScript issues labeled good first issue. The first hundred hits were issues created that day or the next, and one repository filled the top of the list. A ranking by "fewest comments" was mostly ranking tickets that had just been opened. I bounded the search to issues created before October 5 and kept one hit per repository. I also changed a rubric rule that treated a silent maintainer-opened thread as a failed reply. Silence on a maintainer's own issue is not the same thing as ignoring a contributor. After that change, tongs #318 was one of three accepts. Two other issues failed because each already had an open pull request.

The issue had three independent parts. Part 1, the key that cycles recovered review drafts, was already fixed. Part 2 was the README key tables. Part 3 was the contributor check lists. I claimed part 2 only, and said I had not done the comparison yet. The claim is https://github.com/andre-motta/tongs/issues/318#issuecomment-6258495890

The comparison was a file read on Windows 11. I did not create a virtualenv and I did not start the app. I read the README Keybindings section beside `docs/reference/keybindings.md`, and I read `BINDINGS` in `src/tongs/views/repo_list.py`. Four disagreements were still there.

The README said the desktop workspace used labelled controls only. The reference had a Desktop app (beta) key table. The README listed `o` as a global shortcut, "Open in browser." The repository list does not bind `o`. The diff viewer table had no `e` or `F` row. The reference binds `e` and Shift+F. The Pipeline tab had two Escape rows. The reference has one. I posted that comparison at https://github.com/andre-motta/tongs/issues/318#issuecomment-6258522610

The issue also named line numbers in `src/tongs/widgets/diff_panel.py`. In my clone those lines were a banner string, `CHANGES_OVERFLOW_BANNER`, not key bindings. I did not edit that file, and I did not treat those line numbers as the source of the `e` and `F` rows. The reference page was the source of truth the issue itself pointed at.

One sentence in the reference made the `o` row harder than a copy. The intro says the main-screen keys also work on the repository list. The `o` cell says the key is for the inbox and merge-request detail. The issue and the cell agreed with each other, and the repository-list bindings agreed with the cell. I followed the cell. Commit `9ef99be` moved the row out of the Global table and into the Inbox table:

```diff
-| `o` | Open in browser |
+| `o` | Open the current item in the browser |
```

Under MR detail I added a note that `o` opens the current merge request and is not bound on the repository list. The same commit pointed the desktop sentence at the reference's desktop section, added `e` and `F` to the diff viewer, and replaced the two Pipeline Escape rows with the reference's single meaning:

```diff
-| `Escape` | Drill out one level |
-| `Escape` | Close the log search, then drill out one level |
+| `Escape` | Close the log search, or step back one level |
```

No Python and no desktop code changed. The pull request body said this did not close #318, because part 3 was still open, and it named Cursor Grok 4.7 as the tool that drafted the edit.

Before I opened the pull request I ran a local gate. The part I wrote was the manifest: which commands must pass, and which ones I was excluding, with a date and a reason. For this diff the must-pass rows were `python scripts/check_control_chars.py` and the Markdown lint command from the docs CI job. pytest, ruff, the site build, and the desktop lint were excluded on October 18 because the diff did not touch Python, the site, or the desktop app, and this clone had no virtualenv.

The first gate run stopped. Windows `cmd.exe` will not execute the extensionless Unix path `.github/linters/node_modules/.bin/markdownlint-cli2`. I changed the manifest row to the Windows form of that same tool:

```text
.github\linters\node_modules\.bin\markdownlint-cli2.cmd
```

The second run stopped on a file that was not the README. `test_evidence.md` was local notes, untracked, but the lint glob `*.md` still saw it. It had a bare URL and fences with no language. I wrapped the URL and labeled the fences, then ran the gate again. The third run passed. The control-character check reported `No disallowed control characters in 738 text file(s).` Markdown lint reported 54 files and 0 issues. Only then did I open pull request 464 from my fork.

The pull request sat quiet. A monitor run at 2026-10-19T04:18:04Z read it as open for under a day, with zero comments and zero reviews. My playbook says the first nudge waits seven days, so the draft was "No nudge yet. Wait note." I did not post it. The first full monitor run, earlier that evening, had refused to draft at all because the playbook file was still the empty template. I filled the threshold, the one-nudge rule, and the 30-day walk-away, and ran it again.

andre-motta approved and merged 464 at 2026-10-20T00:37:02Z, before any nudge was allowed. His review said: "All four mismatches from part 2 of #318 now match the keybinding reference, and the note about where `o` is bound is a nice touch." He also rewrote the description. GitHub treats the words "close #318" as a closing keyword even after "does not," so my sentence that said the pull request did not close the issue would have closed it. He kept #318 open for part 3. The merge commit on the upstream main branch is `d0d1dbd`.

Part 3 was the remaining work, and I took it after that merge. The pull request template told contributors to run `ruff check src/ tests/`. CONTRIBUTING.md, and the lint job in CI, check more folders and also run `python scripts/check_control_chars.py`. The template did not mention desktop format and lint, or Markdown lint. The site contributing page used the short ruff command too. The README installed `.[dev,lint]`, while CONTRIBUTING.md installed `.[dev,lint,mcp]`, and without the `mcp` extra a local run skips `tests/test_mcp/test_server.py` even though CI runs it. The Documentation changes section said the docs check "lints the Markdown" and did not say how.

Commit `ed79f9e` changed four files. The template, CONTRIBUTING.md, and `docs/contributing.md` now use the same ruff paths as CI: `src/ tests/ packaging/ scripts/ .github/scripts/ examples/`. The template also lists the control-character check, `npm run format:check --prefix desktop`, and `npm run lint --prefix desktop`, and it points the docs item at the Markdown lint commands. Those commands are written out in CONTRIBUTING.md, copied from the docs job:

```text
npm ci --prefix .github/linters --ignore-scripts --no-audit --no-fund
.github/linters/node_modules/.bin/markdownlint-cli2 --config .github/linters/.markdownlint-cli2.jsonc "docs/**/*.md" "*.md" ".agents/**/*.md" ".github/*.md" "site/README.md"
```

The README install extra is now `.[dev,lint,mcp]`, with one sentence pointing at CONTRIBUTING.md. I also added the testing guide's exception that the site build uses a task limit of 256, not 64, because a 64-task limit aborts that build on a machine with many cores.

The gate for this branch failed for a different reason than the Windows path. A run against my local `main` included the already-merged README commit, so the diff looked larger than the four files I had just edited. I reran with `--base upstream/main`. A later run then held the pull request on the disclosure: the description named Cursor Grok 4.7, and the checker was a different model. CONTRIBUTING.md asks for the tool that wrote the commit. I changed my pr-precheck rule so the disclosure is accepted when it matches the `Co-authored-by` trailer, and I quoted that trailer in the description. The next gate passed.

The site build was the other honest gap. A plain `npm run build --prefix site` skipped the docs. On this Windows checkout `site/src/content/docs` is a 13-byte file, not the symlink to `../../docs`. I built again through a junction to `docs/`, with `NODE_OPTIONS=--max-old-space-size=512`. That log included `/contributing/index.html`, 30 pages, and `All internal links are valid.` I did not put the junction command on the gate, because an earlier script that tried to do it inside the gate deleted and restored the docs tree. pytest, ruff, and the desktop checks stayed excluded, dated October 19, because this diff was Markdown only.

Pull request 465 opened with `Fixes #318` on purpose. Parts 1 and 2 had already landed, and this was the last part, so closing the issue was the point. andre-motta merged it at 2026-10-21T00:44:12Z. His review said: "This closes out #318 nicely: the template, CONTRIBUTING.md and the contributing page now list the same checks CI runs, with the exact Markdown lint command and the site build's task limit."

## Limitations and what's next

Both pull requests change documentation. I never started the tongs app, so I did not press `o`, `e`, `F`, or Escape and watch the result. The README now matches the reference and the binding list I read. It does not prove that a future code change will keep the table honest. The local gate caught a bad command path, a messy notes file, a stale base branch, and a disclosure that named the wrong session. It did not catch a wrong key.

The site build on Windows is the sharpest limit. CI follows a symlink. My checkout stores that symlink as a 13-byte file, so a cold `npm run build --prefix site` can exit 0 while publishing almost none of the docs. I proved the contributing page with a junction I built by hand, then removed. The gate itself did not rerun that build.

Next I would add a small check that compares shortcut rows in the README with the binding lists, and leave a human to read cases like `o`, where the reference intro and the reference cell disagree. I would also make the ship-gate base explicit, so a stale local `main` cannot pretend an old commit is part of the new diff, and I would lint local notes before treating a Markdown failure as a problem in the change.
