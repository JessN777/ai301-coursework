# Evidence guide: where proof lives in a reproduction package

## Environment

- Where it lives: In an eval bundle, the **Candidate repro report** (environment paragraph, version banners, `conda info` / `pd.show_versions` blocks) plus any version strings inside command output. The **Issue** body names the reporter's target version/OS; **Repo facts** names what the bug template asks for. In live mode, the student's draft report and the issue's environment section; do not invent versions from other files on disk.
- What good looks like: The attempt can be placed. Software version and OS/platform are named. If the issue is Windows-driver-specific, browser-language-specific, or debug-vs-release-specific, that axis is named too. A log snippet with no OS, no version, and no driver is not an environment record.

## Steps

- Where it lives: The **Candidate repro report** steps, code fences, playground links, and config snippets. Compare them to the **Issue** reproduction steps and trigger syntax. Private-repo caveats in the report count as evidence that a stranger cannot re-run.
- What good looks like: Commands or UI actions start from a stated state and include the issue's actual trigger (the offset-from-end range, the `=` operator, the named driver, the issue's expression). A stranger with only the report could attempt it. "Checked out our private monorepo (cannot share)" is unfollowable.

## Behavior shown

- Where it lives: Fenced output, logs, CSS dumps, screenshots described in the report, exit codes. Read those artifacts against the **Issue** actual/expected behavior, not against the report's narration. The **Thread highlights** can settle what "correct" output looks like.
- What good looks like: The bytes on the page are the bug (or a clear non-occurrence). A `TypeError` matching the issue passes; `error: Invalid value` with exit 1 is not a capacity-overflow crash; a compile error from an unbound `$b` is not an invalid path expression; garbled escape sequences with the process still alive are not a crash; a version banner and tab list are not a blank pane.

## Honesty

- Where it lives: Overlap between the **Candidate claim comment**, the report's result sentence ("reproduced" / "could not reproduce"), and the artifacts. Watch "expected" vs "actual" for inversion. Version lines vs the issue's "confirmed on latest/main" checkboxes live here too.
- What good looks like: The author says exactly what happened. Cannot-reproduce with a real attempt, shown output, and a named difference (ARG_MAX, fish vs zsh, uniform name lengths) is honest and ready. "Guaranteed reproducible" with no measurements is not. Testing pandas 1.5.3 against a latest/main bug without saying so is a silent deviation. A debounce-race diagnosis with no transcript is a claim without backing.

## Comms

- Where it lives: **Candidate claim comment** versus the **Issue** title/body (specificity and intent). **Repo facts** contribution policy / AI policy / bug template. Comments must be checked for disclosure language ("I used an AI assistant…") when the policy requires it, and for human-voiced specificity when the policy bans AI-generated comments.
- What good looks like: The claim names this bug and a next step, and does not promise a fix date or reserve the issue. Disclosure: ghostty-style "all AI usage must be disclosed" fails if the comments stay silent; p5.js-style required disclosure passes when the comment states the tool and that the author ran the steps; conda-style permissive-with-responsibility and "no stated AI policy" pass without a disclosure sentence. Ripgrep-style "comments must be written by humans in their own words" passes a specific, human-voiced claim and fails interchangeable assign-me boilerplate.
