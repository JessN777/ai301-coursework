# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

JessN777

---

## Posted upstream

**Claim comment**

Not posted yet: `gh` is installed but not logged in (`gh auth login` required), so this text is the claim draft that will go on https://github.com/codepath/pathreview-ai301-fa26-s3/issues/73. Replace this sentence with the comment URL after posting.

I'd like to investigate #73: README.md and docs/SETUP.md tell you to set OPENROUTER_API_KEY, but .env.example only documents `mock` / `openai` and OPENAI_API_KEY even though core/config.py defines OpenRouter fields.

I'll follow the documented setup on a fresh clone (copy .env.example, then compare README.md, docs/SETUP.md, .env.example, and core/config.py) and post a report with my environment, the exact commands, and what those files actually contain. I am not promising a fix or a date — just the investigation and the write-up.

Classroom note: classmates have already commented; Path Review house rules say that does not block a claim, so I am posting my own.

I used an AI assistant to help organize this comment; I will run and verify every step myself.

**Reproduction comment**

Not posted yet: same GitHub login blocker as the claim. Text below is the report from the local reproduction at commit `2f4e82f`. Replace this sentence with the comment URL after posting.

## Reproduction report for #73

I reproduced the documentation / `.env.example` mismatch. I did not start the app; this report is only about what the files say after following the documented setup copy step.

### Environment

- OS: Windows 11 (NT 10.0.26200.0)
- Python: 3.12.10
- Git: 2.47.1.windows.2
- Repo: `codepath/pathreview-ai301-fa26-s3`
- Commit: `2f4e82f52efbcfcc57d65b3fa5348672163ca088` (`2f4e82f` on `main`)
- Clone: fresh clone, no other local edits besides copying `.env.example` → `.env` for this check

The issue does not name a runtime version; I used current `main` at the commit above.

### Steps

1. Clone and record HEAD:

```
git clone https://github.com/codepath/pathreview-ai301-fa26-s3.git
cd pathreview-ai301-fa26-s3
git rev-parse HEAD
```

Output: `2f4e82f52efbcfcc57d65b3fa5348672163ca088`

2. What README.md says:

```
findstr /n OPENROUTER_API_KEY README.md
```

Output:

```
24:# Configure environment (add your OPENROUTER_API_KEY to .env)
```

3. What docs/SETUP.md says:

```
findstr /n OPENROUTER_API_KEY docs\SETUP.md
```

Output:

```
47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
```

4. Follow the documented copy step:

```
copy .env.example .env
```

5. LLM-related lines in the copied `.env`:

```
findstr /n "LLM_PROVIDER OPENAI_API_KEY OPENROUTER_API_KEY" .env
```

Output:

```
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
```

6. Search specifically for OPENROUTER_API_KEY in `.env` (no match):

```
findstr OPENROUTER_API_KEY .env
```

Output: no matches.

7. What `.env.example` documents as provider options (lines 16–19):

```
# LLM provider
# Options: "mock" (default, no API key needed), "openai"
LLM_PROVIDER=mock
OPENAI_API_KEY=sk-your-key-here
```

8. What `core/config.py` defines:

```
findstr /n "llm_provider openai_api_key openrouter" core\config.py
```

Output:

```
18:    llm_provider: str = Field(default="mock")
19:    openai_api_key: str = Field(default="")
20:    openrouter_api_key: str = Field(default="")
21:    openrouter_base_url: str = Field(default="https://openrouter.ai/api/v1")
22:    openrouter_model: str = Field(default="google/gemma-3-27b-it:free")
```

### Observed

After `copy .env.example .env`, the resulting `.env` has `LLM_PROVIDER=mock` and `OPENAI_API_KEY=sk-your-key-here` and does not contain `OPENROUTER_API_KEY`. `.env.example` comments list only `mock` and `openai`. README.md line 24 and docs/SETUP.md line 47 still tell you to set `OPENROUTER_API_KEY`. `core/config.py` already has OpenRouter fields.

### Expected

If setup docs tell you to add `OPENROUTER_API_KEY`, `.env.example` should include that variable and list `openrouter` among `LLM_PROVIDER` options, matching what `core/config.py` supports.

### Not tested

I did not run the application, Docker, or OpenRouter. This is a file-consistency mismatch; the commands above are the evidence.

I used an AI assistant to help organize this report; I ran the commands and checked the file contents myself.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. First full harness attempt from `ai301-unit2-starter/eval` crashed before any package verdict: Windows `CreateProcess` could not find `claude` (npm ships `claude.cmd`, not `claude.exe`).
2. Second full attempt found Claude but crashed with `UnicodeEncodeError: 'charmap' codec can't encode character '\U0001f64f'` while sending a package that contains 🙏 on cp1252 stdin.
3. Confirming full run (harness-written `beat-1-sandbox/unit-2/eval-run.txt`, 2026-10-14T03:26:43Z): `python run_eval.py --rubric ~/.claude/skills/repro-check/rubric.md --evidence ~/.claude/skills/repro-check/references/evidence-guide.md --save-run ... --workers 5`. Result: **19/20 scored items, bar PASS**, categories `clear-accept 7/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4`. The only disagreement was pkg-09 (gold accept, rubric reject). I did not loosen checks after that; 19 already clears 18 and the disclosure floor held (pkg-20).

**Package analysis**

pkg-09 (sharkdp/fd#2033), category `clear-accept`. Gold label: **accept**. Rubric verdict: **reject**. Failed checks named by the harness: `steps-followable`, `behavior-matches`, `evidence-backs-claim`.

The package is an honest cannot-reproduce: the author ran the argument-size `--exec-batch` ordering scenario, showed `order.log` as `ONE` then `TWO`, named `ARG_MAX` = 2097152 and uniform ~190-character names as what differed, and did not claim the bug. Gold wants that ready to post. My required `behavior-matches` pass condition says the artifact must display the issue's behavior *or* a cannot-reproduce with a clearly different outcome — the log is a different outcome — but the grader still failed it, reading the missing TWO-before-ONE interleaving as not matching the issue. I am leaving the check wording in place: loosening it would risk flipping wrong-target packages, and the confirming run already passes the bar. Getting pkg-09 "wrong" in this direction (holding an evidenced cannot-reproduce) is the disagreement I am accounting for, not a category the rubric cannot see.

**Check rationale**

`repo-conventions` (required), quoted from the uploaded `tools/repro-check/rubric.md` / `~/.claude/skills/repro-check/rubric.md`:

> If the policy requires disclosing AI usage in issues or comments, the comments disclose it (course packages are AI-assisted work). If the policy only requires human-written comments in the author's own words, pass when the comments are specific and human-voiced rather than generic boilerplate. If there is no AI policy, or a permissive "welcome, you are responsible" policy with no disclosure mandate, this check passes.

This is the disclosure-wall check. The eval set has exactly one such package (pkg-20, ghostty: all AI usage must be disclosed; comments do not). A rubric with no conventions check cannot recover that miss on volume. The same row lets pkg-07 pass (p5.js policy + explicit disclosure) and pkg-05 pass (conda permissive, no disclosure mandate). I kept it required so the category floor cannot be bought back by the other 19.

**Trade-offs**

I kept `behavior-matches` and `steps-followable` strict so wrong-target packages (pkg-02, pkg-08, pkg-16, pkg-17) stay rejects: an adjacent graceful error or an old pandas version is not the issue. The cost is pkg-09, a gold accept that my run held. I did not loosen those checks after the confirming run, because a loosen plus a missed canary is how a 19/20 becomes a floor failure. The other trade-off is accepting an evidenced cannot-reproduce in the pass condition even when the issue's symptom never appears — that is the honest-report path the assignment grades, and pkg-10 (cannot-reproduce on fish vs zsh) did pass.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
