---
status: accepted
date: 2026-08-16
version: 1.0
phase: F1
source: docs/discovery/self-interview.md
method: secondary research (blogs, Logseq forum, Logseq issue tracker), 2026-08-16
---

# Secondary research — corroborating the candidate pains

**Method.** Public writing by Obsidian and Logseq users, the Logseq discussion
forum and issue tracker, searched for independent occurrences of P1-P7.
**Limitation.** Self-selected published opinion, not a representative sample.
It shows a pain *exists* in the wild; it does not size it. No claim here is
quantitative.

## Verdicts

| # | Pain | Verdict | Evidence |
|---|---|---|---|
| P1 | Configuration freedom becomes an unfinishable side-project | **strongly corroborated** | S1, S2, S3, S6 |
| P2 | Heavy capture rituals cause guilt-driven abandonment | **strongly corroborated** | S4, S5, S6 |
| P3 | No natural-language querying of your own notes | **corroborated, crowded** | S5, S7 |
| P6 | Retrieval requires knowing what to ask for | **partially corroborated** | S8, S9 |
| P7 | Task capture needs owner + state | **not found** | — |
| P4 | Graph-wide editing is hard | **not found** | — |
| P5 | No native periodic notes | **weakly corroborated** | S10 |

## Findings

### S1-S3 — The configuration trap is a named, recurring pattern
Multiple independent authors describe the same arc: elaborate setup first,
writing second, burnout third. One describes having spent more time watching
workflow videos and installing plugins than writing, and eventually tearing the
whole vault down. Another names the desire to tweak a tool until it is "perfect"
as a distinct problem category, noting they spent more time configuring than
using. A third describes weeks designing the ideal folder structure before the
first note, with users already burned out by the time they start.

**Reading:** the near-universal advice given to new users is *start with zero
plugins and let structure emerge*. That advice is an admission that the default
configuration of these tools is wrong for most people. A tool that shipped the
advice as its default would need no advice.

### S4-S6 — Abandonment is driven by guilt and overhead, not missing features
One writer describes journaling routines failing through a skip → guilt → skip
loop, quietly quitting while rationalising it. Another argues that most PKM
tools inject structural questions mid-idea, producing decision fatigue and
eventually avoidance. A widely-shared framing is the *write-only system*: saved
to but never read from, where every save feels like progress and the absence of
recall is invisible.

**Reading:** this matches E2/E3 of the self-interview almost exactly, including
the guilt mechanism. This is the strongest signal in F1.

### S7 — Natural-language querying is real demand *and* a crowded answer
Multiple 2025-2026 sources present conversational querying of one's own notes as
the current frontier, and every article criticising the "graveyard" problem
closes by recommending an AI product. Obsidian GPT plugins, Notion AI and
several new entrants already occupy this space.

**Reading:** demand is real (the maintainer's own Cursor workaround is
behavioural proof). But this is where a solo maintainer at 5-10h/week competes
worst, and where differentiation is hardest. Treat as a *bet*, not a given.

### S8-S9 — Query difficulty is a documented Logseq weakness
Logseq's advanced queries are written in Datalog against a Datascript database;
the official docs point users to an external Datalog tutorial and label part of
the reference as being for engineers. A forum thread titled as a rant about
advanced queries complains that available material assumes prior knowledge of
the database schema. The issue tracker also carries reports of multi-property
queries hanging the application on modest graphs.

**Reading:** confirms P6, but reframes it. The problem is not query *syntax*.
Even with perfect syntax, the maintainer reported not knowing what he wants to
see. The gap is between having a question and having a query — which is what
the LLM workaround actually bridges.

### S10 / P4 / P7 — Weak or absent
No independent complaints found about graph-wide editing or task ownership
states. Periodic notes appear only as a solved problem (Obsidian plugin), not as
a lament. These are maintainer-specific preferences until proven otherwise.

## What this changes

1. **The core problem is now defensible:** *these tools push their organisation
   burden onto the user, and the user eventually loses.* P1 and P2 are one
   problem seen from two ends — setup cost and daily upkeep cost.
2. **P4, P5, P7 leave the MVP conversation.** They are maintainer preferences
   without external evidence. Revisit only if real users raise them.
3. **P3 becomes a strategic bet to decide in F2**, not a feature to assume. It is
   the most wanted and the most contested. Tension T2 (offline-first vs LLM)
   must be resolved before it enters scope.
4. **T1 gets new evidence.** One source explicitly lists non-technical users as
   people Obsidian was not built for, citing YAML frontmatter, regex and CSS
   snippets as vocabulary barriers. This is the first external support for the
   maintainer's original "non-technical audience" intuition — but the *pains*
   documented above still come overwhelmingly from experienced users. T1 stays
   open for F2.

## Sources

S1 XDA, "I used Obsidian wrong for months" (2026-02) ·
S2 vanslaars.io, "Note Taking and Writing in Obsidian" (2022) ·
S3 digitalbiztalk.com, "Why Obsidian gets better the longer you use it" (2026-07) ·
S4 dspinosa.substack.com, "Journal++" ·
S5 medium.com/@ann_p, "Your Second Brain Is Broken" (2025-05) ·
S6 dessence.ai, "Why second brains keep becoming graveyards" (2026-07) ·
S7 inkeybit.com, "Building Your Second Brain… 2026" (2026-05) ·
S8 discuss.logseq.com/t/advanced-queries-rant/14083 (2023-01) ·
S9 github.com/logseq/logseq/issues/5213 ·
S10 unmarkdown.com, "Obsidian is Too Complicated" (2026-02)