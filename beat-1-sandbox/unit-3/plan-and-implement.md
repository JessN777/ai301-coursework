# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

JessN777

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73#issuecomment-6162095059

Here is my plan for #73, from my own repro (Windows 11, Python 3.12.10, commit `2f4e82f`).

Diagnosis: `.env.example` never grew `OPENROUTER_API_KEY` when the docs started requiring it. After `copy .env.example .env`, I get `LLM_PROVIDER=mock` and `OPENAI_API_KEY=sk-your-key-here` and no `OPENROUTER_API_KEY`, while README.md:24 and docs/SETUP.md:47 still say to set that key. `core/config.py` already defines the OpenRouter fields, so I am not treating this as a runtime crash (I did not start the app).

Plan: change `.env.example` only — list `openrouter` in the `LLM_PROVIDER` options and add an `OPENROUTER_API_KEY` template line. Out of scope: `core/config.py`, README/SETUP rewrites, Docker, live API calls.

Test: re-run the same copy + findstr checks. After the fix, `findstr OPENROUTER_API_KEY .env` should match, and the provider comment should mention `openrouter`.

I used an AI assistant to help organize this plan; I ran the repro and will make the `.env.example` edit myself.

---

## Your branch

**Branch**

docs/73-openrouter-env-example

**Evidence**

Before (unit 2 repro, commit `2f4e82f` on `main`):

```
copy .env.example .env
findstr /n OPENROUTER_API_KEY README.md
findstr /n OPENROUTER_API_KEY docs\SETUP.md
findstr /n "LLM_PROVIDER OPENAI_API_KEY OPENROUTER_API_KEY" .env
findstr OPENROUTER_API_KEY .env
```

Output:

```
24:# Configure environment (add your OPENROUTER_API_KEY to .env)
47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
OPENROUTER_API_KEY not found in .env
```

`.env.example` provider comment at that time:

```
# Options: "mock" (default, no API key needed), "openai"
```

After (branch `docs/73-openrouter-env-example`, commit `2084f43`):

```
copy .env.example .env
findstr /n OPENROUTER_API_KEY README.md
findstr /n OPENROUTER_API_KEY docs\SETUP.md
findstr /n "LLM_PROVIDER OPENAI_API_KEY OPENROUTER_API_KEY" .env
findstr /n /C:"Options:" .env.example
```

Output:

```
24:# Configure environment (add your OPENROUTER_API_KEY to .env)
47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
20:OPENROUTER_API_KEY=
17:# Options: "mock" (default, no API key needed), "openai", "openrouter"
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Confirming full run from `ai301-unit3-starter-real/eval` (harness-written `beat-1-sandbox/unit-3/eval-run.txt`, 2026-10-14T06:04:36Z): `python run_eval.py --rubric ~/.claude/skills/plan-check/rubric.md --evidence ~/.claude/skills/plan-check/references/evidence-guide.md --procedure ~/.claude/skills/plan-check/procedure.md --save-run ... --workers 5`. Result: **20/20 scored items, bar PASS**, categories `clear-accept 7/7  scope-creep 4/4  thread-convention 2/2  unbuildable 3/3  wrong-cause 4/4`. That agreement line matches the committed `eval-run.txt`. No `--only` loop: the first complete run already cleared 18/20 and the category floor.

**Package analysis**

pkg-20 (ghostty-org/ghostty#11261), category `thread-convention`. Gold label: **reject**. Rubric verdict: **reject**.

The plan itself is a bounded, thread-following crash fix. Gold rejects because ghostty's stated policy requires disclosing all AI usage and the plan comment does not disclose (eval packages are treated as AI-assisted). My `thread-conventions` check fails a comment that omits required disclosure, so the package is held even though diagnosis, scope, files, and tests would pass. That is the 2-item category a rubric with no comment-vs-conventions check cannot see.

**Check rationale**

`thread-conventions` (required), quoted from the uploaded `tools/plan-check/rubric.md`:

> If a maintainer in the thread already isolated a file, posted a patch, or asked for a specific test, the comment engages that direction rather than substituting an unrelated workaround. If the repo-facts policy requires disclosing AI usage in issues or comments, the plan comment discloses it (eval packages are AI-assisted work). If the policy only requires human-written comments, pass when the comment is specific and human-voiced. If there is no AI-disclosure mandate and no ignored maintainer direction, this check passes.

I wrote it as one required row so the floor cannot be missed: pkg-04 (docs-only workaround that ignores the owner's `light_windows.go` patch) and pkg-20 (missing ghostty disclosure) are different surfaces of the same family. Splitting them would have been prettier; bundling them is what keeps a silent AI-policy miss from being bought back on volume.

**Trade-offs**

Bundling thread-direction and AI disclosure in one check means a package could fail for either reason, and the harness `note` will not distinguish them. I accept that: the verdict is still hold, which is what gold wants for both pkg-04 and pkg-20. Loosening the disclosure half would need a pkg-20 canary on `--only` before another full run; I did not loosen, because the confirming run already agreed on 20/20 including `thread-convention 2/2`.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
