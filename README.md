## Mike Fornal

I build production AI systems end to end, alone, and I mostly do it in unglamorous
places: pharmaceutical R&D rigs, connected-car hardware, bank post-trade plumbing,
and the applicant tracking systems nobody reads twice.

Marlborough, MA · [forn.al](https://forn.al) · [LinkedIn](https://www.linkedin.com/in/michael-fornal/)

---

### What I've built

**[job-net](https://github.com/MichaelFornal/job-net)** · public · Python

A job-market crawler, corpus and triage system: 43 ATS crawlers behind one row
contract, three-tier dedupe, posted-date provenance, and a keyboard-driven review app.
Four third-party dependencies. Everything else is the standard library. `make demo`
seeds a synthetic database and serves the app in two minutes, with no keys, no corpus
and no network.

This is the published slice of a larger private system. The full deployment indexes
**6,119,824 postings** from **141,921 companies** across **86 sources** and **136,518
ATS boards**, refreshed daily by one command. The identity resolver parses ATS identity
out of apply URLs across **24 platforms** and collapses **3,013,608 duplicate rows**
into canonical records.

None of those numbers were typed. A counter re-runs all of them and records the command
beside each figure, because on 2026-08-14 I published two numbers that had both been
produced by a command and were both wrong: the command was pointed at a log file that a
later rebuild had superseded. Counted is not the same as current.

**[GPTee](https://gpett.com)** · live · TypeScript, Deno, Postgres, React

An AI-native print-on-demand storefront I built and operate solo: **~314,000 lines** of
TypeScript and React, **225** serverless edge functions, **207** database migrations,
two storefronts on one backend, live payments and creator payouts. Generation runs
through Michelangelo, a multi-model pipeline that routes each task by quality, latency
and cost: Claude for agentic tool calling and vision QA, Gemini for generation,
Replicate for post-processing. Prompt to production asset in about thirty seconds.

Evaluation went in before launch, not after. Agent persona test suites, output drift
detection, vision-based moderation, and scoring harnesses that catch prompt and model
regressions in CI instead of in front of a customer. So did the cost guards: per-call
budget enforcement and a four-tier budget guard, because an image model with no ceiling
is a bill, not a feature.

**[forn.al](https://forn.al)** · live

My site. Hand-written HTML with no JavaScript at all; the CSP forbids it. Every number
on it is checked against the counter by a build gate that fails if the page and the
count disagree.

---

### How I work

Zero-to-shipped alone, across the whole stack and the business around it, and fluent
enough in a hard domain to build in it. I go deep on niches before they get crowded.

I try to be honest about what the numbers say, including when they say I was wrong.
I built an LLM pipeline to draft and fill job applications end to end, then measured it
against the event log instead of against its own config: **49 attempts, 7 clean fills,
6.2 minutes per attempt, 42 minutes per completed application.** Doing the same work by
hand takes about four. So the pipeline is a drafting tool now and not an autopilot, and
the 357 required fields it left blank turned out to be unanswered questions rather than
bugs.

The guards I kept all fail the same direction. Numeric grounding, metric retention,
topic-drift detection and evidence-bound answers each fall back to the hand-written
version when they trip, because over-rejecting is cheap and a fabricated number in an
interview is not.

I wrote up how I think about this at more length in
**[eval-harness.md](eval-harness.md)**: measuring whether an agent actually replaced the
work, rather than whether the model looked good doing it.

Most of what I ship is built with Claude Code. The interesting part was never the
prompting. It was the verification patterns that keep a multi-pipeline codebase coherent
across sessions.

---

### Before this

Tokenization and digital-asset advisory for global banks at Capgemini, under the EVP of
Capital Markets, plus early enterprise Gen AI work there from late 2022. First US
commercial hire at a UK fund-finance marketplace. Ops data science at DIMO, onboarding
the first thousand customers onto physical connected-car hardware. Before all of it, a
Python-to-Power-BI pipeline at Lyndra Therapeutics that replaced an Excel workflow
costing analysts hours a week, where the real blocker turned out to be inconsistent
test-ID conventions across teams rather than the model.

B.S. Data Science, Bryant University.
