---
status: accepted
date: 2026-08-16
version: 1.0
phase: F1
source: copilot interview session, 2026-08-16
next: docs/discovery/secondary-research.md (F1.2)
---

# Self-interview — maintainer as user

**Method:** structured interview about past episodes, not desired features.
**Sample:** n=1, the maintainer. Strong self-selection bias; every finding here
is a *candidate* pain, to be corroborated in F1.2 before informing strategy.

## Subject profile

~1 year on Obsidian (first PKM contact), then migrated to Logseq, current daily
user. Tech Lead. Reconfigured templates and strategies many times in both tools.

## Behavioural evidence

### E1 — The problem survived the tool change
Reconfigured repeatedly in Obsidian; migrated to Logseq; reconfigured again.
The migration was motivated by *"I was doing noticeably less configuration"* —
not by a missing feature. The recurring cost is the freedom to configure, not
any particular configuration.

### E2 — The abandonment cycle is guilt, not missing features
Self-designed daily template with many fields → subject sensed most of the
captured data would never be read → hesitated on what belonged → ended days
incomplete → next morning spent finishing yesterday → sessions grew long →
usage declined. No feature gap appears anywhere in this loop.

### E3 — One practice survived both migrations; one failed and was replaced
**Survived:** Eisenhower via `#important` / `#urgent` tags, with a **single
view where all captured tasks appear**. Described as working well.

**Failed:** transcribing Google Meet notes into Logseq with people tagged. The
subject describes it as frustrating and it did not survive.

**What replaced it** is the more informative finding — a deliberately narrow
capture schema, self-imposed:
- only what is *relevant* is written down (not the full meeting record);
- the person involved is tagged;
- each item is classified as **my action** or **waiting on someone**.

The subject reduced an open-ended capture to a fixed, opinionated schema, and
only then did the practice stick. This is P2 resolving itself through
constraint, and it is the strongest available evidence that strong defaults
outperform expressive freedom for this user.

### E4 — The escape hatch is always *outside* the app
Every unmet need was solved by leaving the tool, never by configuring it deeper:
- Querying own notes → opens **Cursor** on the journals folder
  (e.g. "what was the link Pedro sent?", "summarise the last two weeks in
  bullets for the retro"). ~3 min per query; friction is *re-structuring the
  prompt every time*. Spent ~2h building a reusable Skill for the retro summary,
  having procrastinated on it for days.
- Find-and-replace across the graph (fixing a typo, improving wording) → Cursor,
  because Logseq makes it hard.

### E5 — Imposed opinions were resisted, then accepted
Logseq imposes outline-everything, journal-first, no folder hierarchy. Subject
initially resisted only one — not being able to see a list of journals/notes —
then adapted and concluded it was unnecessary. No plugin, no workaround, no
regret. **A strong default won over the user's initial preference.**

### E6 — Stated gaps
- Logseq queries are hard to write, *and* the subject is unsure what he wants to
  see. The second half matters more than the first: better query syntax would
  not solve "I don't know what to ask for".
- No native weekly/monthly/yearly notes (Obsidian has it via plugin).

## Candidate pains (unvalidated)

| # | Pain | Evidence | Confidence |
|---|---|---|---|
| P1 | Configuration freedom becomes an unfinishable side-project | E1, E2 | high (behavioural, twice) |
| P2 | Open-ended capture rituals grow heavier than their payoff, causing guilt-driven abandonment; narrow, opinionated schemas survive | E2, E3 | high |
| P3 | No way to ask questions of your own notes in natural language | E4 | high |
| P4 | Editing across the whole graph (rename, rewrite, fix typo) is hard | E4 | medium |
| P5 | No native periodic notes above the daily | E6 | medium |
| P6 | Retrieval requires knowing what to query for | E4, E6 | medium |
| P7 | Task capture is only useful when tied to an owner and a state (mine / waiting on someone) — not present natively in current tools | E3 | medium |

## Tensions to resolve in F2 / F4

- **T1 — ICP contradiction.** These pains belong to an experienced PKM power user,
  not to the "non-technical people" audience assumed at project start. The two
  are different products. Unresolved. `[ASSUMPTION]`
- **T2 — Offline-first vs LLM.** P3 is the hottest signal but pulls against the
  offline-first and lightness constraints: a local model is heavy, a remote API
  breaks offline-first and sends personal notes to a third party. Unresolved.
- **T3 — Opinionated vs power-user needs.** P4 and P5 are the kind of request
  normally answered with plugins or settings. Scope is deliberately closed
  (ADR 0002), so each must be answered by a default or refused outright.

## What this does not tell us

Whether anyone other than the maintainer feels P1–P6, and whether they feel them
strongly enough to switch tools. That is the job of F1.2.