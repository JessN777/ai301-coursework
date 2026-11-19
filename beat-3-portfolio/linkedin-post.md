I fixed the keyboard shortcut tables in the README of tongs, an open source tool for reviewing code changes. The tables disagreed with the project's own reference, so a reader could follow a shortcut that the app did not actually use.

I compared the README with the reference and with the list of keys in the code, then changed only the README. A local check stopped me twice before I opened the pull request: once because a documentation command would not run on Windows, and once because my own notes failed the same check as the files I was changing. I fixed both and opened the request only after the check passed. The maintainer reviewed it, confirmed the four mismatches were gone, and merged it on October 19, 2026. A second, separate pull request later finished the rest of the same issue.

The work taught me to treat a failed check as information. The first failure was the command, not the README. Writing down what I did not run mattered as much as what I did run.

https://github.com/andre-motta/tongs/pull/464

#opensource #documentation
