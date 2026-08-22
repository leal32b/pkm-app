---
status: accepted
date: 2026-08-16
version: 1.0
phase: F2
source: maintainer's three daily-note templates (Obsidian ~2024, Logseq v1, Logseq current)
relates: docs/discovery/self-interview.md, docs/discovery/experiments/e1-alt-passive-listening.md
---

# Template archaeology

Three generations of the maintainer's daily-note template, evolved over roughly
two years of real use. This is the strongest evidence the project has: not
opinion about what a good system would be, but a record of what survived
sustained daily use and what was cut.

**Status of the evidence.** n=1, and the subject is the product's author. But it
is *longitudinal behaviour*, and the third generation has two months of reported
higher productivity behind it. It is the closest thing to a validated design
this project will get before shipping.

## The measurements

| | Obsidian (gen 1) | Logseq (gen 2) | Logseq (gen 3, current) |
|---|---|---|---|
| Sections | 7 | 9 | **4** |
| Automated views | 4 | 2 | **1** |
| Prompted fields to fill | 10 recurring checkboxes | 8 (3 in, 5 out) | **2 in, 4 verifications** |
| Dedicated capture buckets | Anotações, Agenda | Inbox, Decisions, Blocks/Risks, Learnings | **none — one stream** |

## What survived all three generations

Only three things. They are the product's skeleton.

1. **Intent, declared before the day starts.** "Foco do dia" appears in every
   generation. It narrowed from linked P0/P1/P2 to three unlabelled slots —
   the *limit* survived, the *ranking* was cut.
2. **One undifferentiated stream for the day.** Called Anotações, then Activity
   log, then Activity log. Always present, always free-form.
3. **A closing ritual.** Present in all three, but its nature changed completely
   (see below).

## What was cut, and what each cut teaches

### C1 — Dedicated buckets → inline tags on one stream
Gen 2 had separate sections for Decisions, Blocks/Risks/Incidents, and
Learnings/Insights, plus an Inbox. Gen 3 has none of them. Instead, everything
is written into the single Activity log and marked inline with one of five tags
(decision, risk, blocker, learned, insight); a single query gathers them back
into a Highlights view.

**This is the central design move.** It removes the "where does this go?"
decision at the moment of capture — opportunity O1.1 — while *keeping* the
structure, by deferring classification to a mark and collection to a view.
Capture stays cheap; retrieval stays structured.

### C2 — Self-measurement died
Energy ratings at the start and end of the day (gen 2) are gone. Data that was
collected and never acted on. **Do not measure what will not be used.**

### C3 — Reflection prompts died
Gen 2's closing asked five questions: the most important decision, who on the
team needs attention, something that should have been delegated, tomorrow's
first action. Gen 1 asked what was learned about product, technical work and
leadership. **All cut.**

These are precisely the *aspirational capture* identified in E1-alt: homework
filed against a future self who will process it. This is independent behavioural
confirmation of the re-scoping of O2.2 — the enemy is not volume of capture, it
is capture that exists to satisfy a method.

### C4 — The closing ritual changed kind, not just size
Gen 1 and 2 closed with **work to do** (read Slack, check email, answer prompts).
Gen 3 closes with **four verifications** — was the focus completed, was the
intention reached, does the log have owners and statuses, is everything captured.

The closing stopped being a task list and became an **audit of the day's own
fields**. It is the mechanism that stops incomplete days from becoming next
morning's debt (O2.1).

### C5 — Automated views collapsed from four to one
Gen 1 displayed memories from this date in past years, notes created today, and
tasks completed today. All gone. The surviving view shows only **what the user
explicitly marked as important**.

**Generated views are noise unless the user marked the content.** The one
surviving query is not automatic discovery — it is retrieval of a deliberate act.

### C6 — Ranking, delegation and the inbox died
P0/P1/P2 became three equal slots. "What can I delegate today?" gone. The Inbox
gone. Each was a decision the user had to make daily and stopped making.

## Extracted design principles

Candidates for the product's core. Each is derived from a cut, not invented.

- **P-A One stream, not many buckets.** There is exactly one place to write.
- **P-B Classify by marking, not by filing.** Structure is added inline, after
  the thought, never before it.
- **P-C Views show only what was marked.** No automatic surfacing of unmarked
  content.
- **P-D Intent is declared, and it is capped.** Three focus slots, one intention.
  A limit, not a ranking.
- **P-E The day closes with an audit, not with homework.** Verify the fields;
  never ask a reflective question.
- **P-F Never collect what will not be used.**

## The open question this raises

The surviving template is **work-specific**: a Tech Lead's day, with team
members, decisions, blockers and delegation. It is not a general-purpose PKM
template. Whether the product should follow it there — becoming an opinionated
work journal rather than a general PKM — is undecided and belongs to the
rewritten vision.

## The vocabulary problem

Three tag vocabularies now exist in the maintainer's system, invented at
different times for different needs:

- Highlights: decision, risk, blocker, learned, insight
- Meetings (self-interview E3): person, my action / waiting on someone
- Eisenhower: important, urgent

An opinionated product must ship **one** vocabulary, or a deliberate few.
Reconciling these is a F3 design task, and it is where the product's opinion
becomes concrete.