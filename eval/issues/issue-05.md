# Eval item: issue-05

- source: sympy/sympy#28806
- captured: 2026-08-05
- calibration: false

## Repo facts (captured 2026-08-05)

- repo: sympy/sympy (14832 stars, archived: no)
- description: A computer algebra system written in pure Python
- last push to any branch: 2026-08-04
- latest release: 1.14.0 (2025-04-27)
- open issues + PRs: 5910
- last 5 default-branch commits:
  - 2026-08-04 by asmeurer: Merge pull request #30204 from oscarbenjamin/pr_scipy_matrix
  - 2026-08-03 by oscarbenjamin: fix(lambdify): use scipy sparse arrays
  - 2026-08-03 by oscarbenjamin: fix: Use scipy sparse arrays instead of sparse matrices
  - 2026-08-03 by moorepants: Merge pull request #29830 from moorepants/lagrange-efficiency
  - 2026-07-31 by Upabjojr: Merge pull request #29829 from Woodman04/euler
- maintainer first-response sample (5 recently updated issues, days to first owner/member/collaborator comment):
  - #23858 (opened 2022-07-29): 0.5 days
  - #23028 (opened 2022-02-06 by a maintainer): 7.4 days
  - #30198 (opened 2026-08-03 by a maintainer): no maintainer comment in thread
  - #30183 (opened 2026-07-31): no maintainer comment in thread
  - #30210 (opened 2026-08-03): 0.0 days
- contribution policy (CONTRIBUTING.md): no statement on AI or contribution tooling
- this issue: assignees: none; linked PRs: sympy/sympy#28807 (merged); sympy/sympy#28813 (merged); sympy/sympy#28815 (open); sympy/sympy#28817 (open); sympy/sympy#28829 (closed); sympy/sympy#28832 (merged); sympy/sympy#28839 (open); sympy/sympy#28847 (closed); sympy/sympy#28875 (closed); sympy/sympy#28876 (closed); sympy/sympy#28877 (merged); sympy/sympy#28878 (merged)

## Issue

### Adding more type annotations to the codebase (#28806)

opened by oscarbenjamin (COLLABORATOR) on 2025-12-21, state open, labels: Easy to Fix, good first issue, typing

There is a long discussion in gh-17945 about adding type annotations to the sympy codebase but that is more of a historical issue with many tangents. Some parts of the codebase now have type annotations and this issue is about incrementally adding more type annotations. PRs are welcome both big and small (better to start small) that add type annotations to parts of the codebase where it makes sense to do so (not necessarily anywhere in the codebase - see below).

You can see related issues and PRs under the typing label:
`https://github.com/sympy/sympy/issues?q=label%3A%22typing%22`

[PEP 484](https://peps.python.org/pep-0484/) introduced type annotations to Python but the sympy codebase predates that and so did not have type annotations when most parts were written. Over time the role of type annotations in Python has become a bit clearer and the situation is that type annotations are basically not optional for a library like SymPy especially on public interfaces. Many users of SymPy will not necessarily use type annotations much in their own code but can still benefit from type checker based tools for things like autocomplete and for checking types in their own code. You can see an examples of this in my editor:

[content truncated - see original fetch for full details]

## Comments (106 total, first 40 shown)

[comments truncated - see original fetch for full details]
