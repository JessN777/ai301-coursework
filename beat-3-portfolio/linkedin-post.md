I brought two sets of tongs docs into agreement with the project itself. The README listed keyboard shortcuts the reference did not, and the contributor check lists were shorter than the checks CI actually runs.

I compared the shortcut tables with the reference and with the key list in the code, then changed only the README. A local check stopped me twice before I opened the pull request: once because a documentation command would not run on Windows, and once because my own notes failed the same check as the files I was changing. I fixed both and opened the request only after the check passed. The maintainer merged that fix on October 19, 2026, and kept the issue open for the check lists. A second pull request made the template and the contributor guides name the same commands CI runs. He merged it the next night, and the issue closed.

The work taught me to treat a failed check as information. The first failure was the command, not the README. Writing down what I did not run mattered as much as what I did run.

https://github.com/andre-motta/tongs/pull/464

#opensource #documentation
