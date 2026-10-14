# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

- Where it lives: Eval: **Candidate plan** cause/diagnosis sentences, plus the **Repro evidence** block (steps, observed, expected, control runs). The **Issue** body names the reported bug. Live: `plan.md` Diagnosis, and the student's posted repro comment (or a house repro pack quoted in the drafts).
- What good looks like: The stated cause cites behavior the repro actually showed. A control that still works (no `-v`, instance-method error still prints, collect synthesizes null, zeros already gone before the cast) means a plan that blames the ruled-out layer fails. "Poke around this weekend" is no diagnosis.

## Scope

- Where it lives: Eval: plan in-scope / out-of-scope / "Change:" / files list / approach bullets. Compare to the **Issue** (what it asked) and any maintainer settlement in **Thread highlights**. Live: `plan.md` Scope and Files I'll touch.
- What good looks like: One bounded change (one file, one callback, one constant, one grouping site). Explicit "out: migrations / other views / tombstone rework" is ready. A five-front campaign, printer rewrite, Transition state-machine, undici migration, or new option bundled with the fix is scope creep even if the core diagnosis is right.

## Executability

- Where it lives: Eval: plan file paths, function/module names, ordered approach. Live: `plan.md` Approach and Files I'll touch.
- What good looks like: A stranger can open a named file and start. `pkg/gui/controllers/sync_controller.go` plus "add commits context to post-push refresh" is enough. "Profile-and-optimize", "gocui? tcell? not sure", "recover() somewhere", "upstream or vendored, whichever is easier" are not.

## Test plan

- Where it lives: Eval: plan Test / Test plan section, read against **Repro evidence** steps and artifacts. Live: `plan.md` Test plan.
- What good looks like: Re-run the repro and name the after-fix observable (exit 0, color flips at step 3 without leaving the view, backdated cache miss, issue cases as regression tests). "Should feel fast", "nothing else should feel broken", or "run the full test suite" with no observable for this fix is not decisive.

## Honesty

- Where it lives: Eval: plan risks, unknowns, checked-unknowns, Deviations. Live: `plan.md` Risks and unknowns and `## Deviations`.
- What good looks like: Named unknowns (tool-by-tool `--` support, untestable Windows variant) with the chosen slice still buildable. False confidence is a diagnosis that ignores a control run. A filled Deviations section after the build (including "nothing changed") is honest; a blank one after a diverging diff is not.

## Comms

- Where it lives: Eval: **Candidate plan comment** vs **Thread highlights** and **Repo facts** (CONTRIBUTING, AI policy, bug template). Live: `comment.md`, the issue thread, and the repo's contributing/AI docs.
- What good looks like: The comment is this issue's plan in the author's words, not "same approach as above". If a maintainer isolated `src/tui/light_windows.go` and asked that a patched binary be tested, a docs-only workaround comment fails. If policy requires disclosing all AI usage (ghostty), the comment discloses the tool and extent. Permissive-or-silent AI policy passes without a disclosure sentence; human-voiced-comments-only policy passes a specific comment and fails boilerplate.
