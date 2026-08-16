---
status: accepted
date: 2026-08-16
version: 1.0
phase: F1 (closing artifact)
source: docs/discovery/self-interview.md, docs/discovery/secondary-research.md, docs/discovery/competitive-analysis.md
next: F2 — docs/product/vision.md
---

# Opportunity map

Structured after Teresa Torres' opportunity solution tree, **opportunity side only**.
Solutions are deliberately absent; they belong to F3. Writing a solution here is
how a discovery phase turns into a feature list.

## Desired outcome

> **The user still uses the app in month six.**

Chosen because every pain found in F1 ends the same way: abandonment. Not
missing features, not switching to a better tool — quiet decay. Retention over
months is therefore the only outcome that proves the problem was solved.

Leading indicator, to be defined in F2: *days used per week, in week 12 vs week 1.*

## Target: who this is for

Not "non-technical people" — that framing was an assumption at project start and
found no support in the evidence. The pains documented belong to people who
**already run a PKM and are losing to it**:

- have used Obsidian, Logseq, Notion or Roam for months or years;
- have rebuilt their setup at least once;
- are currently in decline of use, or feel guilt about it;
- a subset has just been told their file-based Logseq is in maintenance-only mode.

Narrow, reachable, and it includes the maintainer. To be formalised as the ICP in F2.

## Opportunities

### O1 — "Setting up the system became the project" `[highest confidence]`
The tool's configurability turns into an open-ended side-project that competes
with the work it was supposed to support.

- **O1.1** Deciding *where a note goes* costs attention at the moment of capture.
- **O1.2** The setup is never finished — there is always a better arrangement.
- **O1.3** Switching tools does not help; the burden migrates with the user.
- **O1.4** New users face a blank canvas with no default path.

Evidence: self-interview E1, E5 · secondary S1-S3, S10 · competitive gap
(every low-setup competitor is closed source and paid).

### O2 — "My daily ritual costs more than it returns" `[highest confidence]`
Capture routines grow until completing them is a chore, producing guilt, then
skipped days, then abandonment.

- **O2.1** Incomplete days accumulate as debt, paid at the start of the next day.
- **O2.2** The user senses most captured data will never be read, and captures anyway.
- **O2.3** Guilt, not dissatisfaction, is what ends usage.
- **O2.4** A narrow, imposed capture schema survives where an open one does not.

Evidence: self-interview E2, E3 · secondary S4-S6.

### O3 — "I cannot ask my own notes a question" `[high demand, high competition]`
Retrieval requires the user to already know what to look for and how to express
it. The gap is between *having a question* and *having a query*.

- **O3.1** Query languages are a barrier (Logseq's advanced queries are Datalog).
- **O3.2** Even with perfect syntax, the user does not know what to ask for.
- **O3.3** The workaround is to leave the app entirely (Cursor over the notes folder).
- **O3.4** Recall is the point: a write-only system is a graveyard.

Evidence: self-interview E4, E6 · secondary S5, S7-S9.
**Contested:** this is the most crowded quadrant in the market and pulls against
offline-first (tension T2).

### O4 — "The app itself gets in the way" `[low confidence, keep watching]`
Performance, editing across the whole graph, periodic notes. Individually weak
evidence; grouped here so they are not lost.

Evidence: self-interview E4 (P4), E6 (P5) · scattered third-party complaints
about Logseq typing lag and query performance. Not a basis for the MVP.

## Priority

| | Opportunity | Evidence | Market position | Fit for a solo maintainer |
|---|---|---|---|---|
| 1 | **O2** | strongest | unoccupied | high — product design, not technology |
| 2 | **O1** | strong | unoccupied | high — mostly restraint |
| 3 | O3 | strong | crowded | low — funded competitors, heavy tech |
| 4 | O4 | weak | n/a | n/a |

**O1 and O2 are one problem seen from two ends:** setup cost and daily upkeep
cost. Together they are the project's thesis — *the app decides, so the user does
not have to* — and both sit in the empty quadrant identified in F1.2b.

**O3 is deliberately ranked below its demand.** It is the most attractive and the
worst-matched to this project's constraints. It is a candidate *bet*, to be
argued explicitly in F2, not assumed into scope.

## Open tensions carried into F2

- **T1 — ICP.** Effectively resolved in direction (experienced, declining PKM
  users), to be formalised.
- **T2 — Offline-first vs LLM.** Blocks any decision on O3.
- **T3 — Opinionated vs power users.** O1/O2 imply refusing configuration; the
  target audience is precisely the group most used to configuring. Unresolved,
  and the single biggest risk to the thesis.

## F1 gate

Met. Three documented pain clusters with independent external corroboration, a
named target population, a prioritisation with stated rationale, and three
explicit tensions carried forward rather than assumed away.

Not met, and honestly so: **no first-hand contact with a user other than the
maintainer.** Every finding here is either self-observation or public writing.
F2 must include at least one cheap experiment that puts the thesis in front of
a real stranger.