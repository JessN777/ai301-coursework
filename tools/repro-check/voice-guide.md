# Voice guide: how I talk upstream

## Who I am in threads

I am a course student making a first contribution on Path Review. I
have Python experience and I am still learning this codebase. Readers
should expect a specific investigation plan, then a report of what I
actually ran, not a promised patch or a reserved issue.

## Rules I write by

### Rule: Promise the report, never the fix

I claim work by saying what I will investigate and that I will post
what I find. I do not promise a patch, a merge, or a calendar date.

- Wrong: "Assign this to me, I will fix it within 2 days guaranteed."
- Right: "I'll follow the documented setup on a fresh clone, compare README.md, .env.example, and core/config.py, and report what I find."

### Rule: Do not assert a reproduction in the claim

The claim goes up before I reproduce. The claim names the issue and the
next steps. It does not say I already confirmed the bug unless the repro
comment is already written and posted with it.

- Wrong: "I reproduced this and the bug is definitely in config.py."
- Right: "I'll investigate this documentation mismatch and come back with environment, steps, and what the files actually contain."

### Rule: Write my own proof, even on a shared issue

I never piggyback. If classmates already posted, I still describe my
environment, my commands, and my output in my own words.

- Wrong: "Same as above, can confirm."
- Right: "On Windows 11, Python 3.12, commit 2f4e82f, `cp .env.example .env` then `findstr OPENROUTER .env` returned no matches, while README line 24 still tells you to add OPENROUTER_API_KEY."

### Rule: Say only what the artifact shows

If I did not start the app, I say so. If I could not reproduce, I say
so and show the attempt. I do not upgrade a file mismatch into a
runtime failure or a guess into a root cause.

- Wrong: "The app crashes on startup because OpenRouter is missing from .env.example."
- Right: "I did not start the app. After copying .env.example, the file has OPENAI_API_KEY and no OPENROUTER_API_KEY, which is the mismatch the issue describes."

### Rule: Stay inside this issue

I name the files, keys, and behavior in #73. I do not use interchangeable
"great project, please assign me" boilerplate that could be pasted on
any ticket.

- Wrong: "Hello sir! Great project, this looks like a good one for me."
- Right: "Issue #73: README and docs/SETUP.md tell you to set OPENROUTER_API_KEY, but .env.example only documents mock/openai and OPENAI_API_KEY. I'll check those three files plus core/config.py on a fresh clone."

## Things I never post

- A guaranteed fix, ETA, or "keep this reserved for me"
- "+1" / "same as above" with no steps of my own
- A root cause I did not observe
- A claim that I already reproduced, written before I ran anything
- AI-generated enthusiasm padding ("huge usability problem", "top priority for the next release")
