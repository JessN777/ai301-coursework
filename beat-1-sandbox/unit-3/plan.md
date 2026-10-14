# Plan: README and `.env.example` disagree about which LLM API key to set (#73)

## Diagnosis

`.env.example` was never updated when the docs started telling people to set `OPENROUTER_API_KEY`. `core/config.py` already defines OpenRouter fields, but the example env file still documents only `mock` / `openai` and `OPENAI_API_KEY`. Copying `.env.example` to `.env` therefore cannot produce the key the README and SETUP tell you to add. This is a docs/example mismatch, not a runtime crash.

Repro evidence I rely on (quoted from my unit 2 report on #73):

> After `copy .env.example .env`, the resulting `.env` has `LLM_PROVIDER=mock` and `OPENAI_API_KEY=sk-your-key-here` and does not contain `OPENROUTER_API_KEY`. `.env.example` comments list only `mock` and `openai`. README.md line 24 and docs/SETUP.md line 47 still tell you to set `OPENROUTER_API_KEY`. `core/config.py` already has OpenRouter fields.
>
> ```
> 24:# Configure environment (add your OPENROUTER_API_KEY to .env)
> 47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
> 18:LLM_PROVIDER=mock
> 19:OPENAI_API_KEY=sk-your-key-here
> ```
>
> I did not start the app. This is a file-consistency mismatch.

## Scope

In scope: make `.env.example` agree with the documented OpenRouter setup — add `OPENROUTER_API_KEY` and list `openrouter` among `LLM_PROVIDER` options.

Not in scope: changing `core/config.py` (it already has the fields), rewriting README.md or docs/SETUP.md, adding runtime OpenRouter tests, or starting Docker / the app. The issue names README.md and `.env.example`; the missing piece after the repro is the example file.

## Files I'll touch

- `.env.example`: add an `OPENROUTER_API_KEY` template line and mention `openrouter` in the `LLM_PROVIDER` comment.

## Approach

1. Edit the LLM provider comment in `.env.example` so options include `openrouter`.
2. Add `OPENROUTER_API_KEY=` (empty or placeholder) next to `OPENAI_API_KEY`.
3. Re-run the unit 2 findstr / copy checks on a clean copy of `.env.example`.

## Test plan

Re-run the repro steps after the fix:

1. `copy .env.example .env` (overwrite the previous copy).
2. `findstr /n OPENROUTER_API_KEY README.md`
3. `findstr /n OPENROUTER_API_KEY docs\SETUP.md`
4. `findstr /n "LLM_PROVIDER OPENAI_API_KEY OPENROUTER_API_KEY" .env`
5. `findstr /n "llm_provider openai_api_key openrouter" core\config.py`

Before the fix I saw: README:24 and SETUP:47 mention `OPENROUTER_API_KEY`; copied `.env` had only `LLM_PROVIDER=mock` and `OPENAI_API_KEY=sk-your-key-here` (no `OPENROUTER_API_KEY`); `.env.example` options were `"mock" ... "openai"` only.

After the fix I expect: the same README and SETUP lines still mention `OPENROUTER_API_KEY`; `findstr OPENROUTER_API_KEY .env` matches a line; `.env.example` / copied `.env` comments list `openrouter` as a provider option. I still will not start the app.

## Risks and unknowns

- Whether maintainers want a commented-out key vs an empty value; I will use an empty/placeholder line matching `OPENAI_API_KEY`'s style.
- I am not verifying live OpenRouter calls.

## Deviations

Nothing changed from this plan. The build was the `.env.example` edit described above: the `LLM_PROVIDER` comment now lists `openrouter`, and `OPENROUTER_API_KEY=` sits next to `OPENAI_API_KEY`. I did not touch `core/config.py`, README.md, or docs/SETUP.md, and I still did not start the app. After `copy .env.example .env`, `findstr` shows line 20 `OPENROUTER_API_KEY=` on the copied `.env`.
