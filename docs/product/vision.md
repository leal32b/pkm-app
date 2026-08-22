---
status: accepted
date: 2026-08-22
version: 0.2
phase: F2
supersedes: vision.md v0.1 (2026-08-16)
source: docs/discovery/opportunity-map.md, docs/discovery/template-archaeology.md,
        docs/discovery/experiments/e1-alt-passive-listening.md,
        docs/discovery/market-pain-research.md
---

# Product vision

## One line

**Day one of this app is where I arrived after two years of trial and error.**

## The bet (revised)

The v0.1 framing — *the app removes configuration* — was weakened by evidence:
the target audience already solves the configuration trap with self-discipline,
inside flexible tools, at no cost. Competing against free self-restraint is a
losing position (see E1-alt).

The revised bet is narrower and survives that evidence: **self-discipline works,
but it is paid for in years.** The maintainer's own daily template took roughly
two years and two tool migrations to converge, and each convergence step removed
something. Others in the same audience report similar arcs — most only reaching
a workable system after abandoning one. The product does not sell the absence of
options. **It sells a destination.**

The corollary is uncomfortable and accepted: **the destination has to be right.**
There is no plugin ecosystem and no settings screen to absorb a wrong default.

## Design principles

Derived from what survived two years of daily use (`template-archaeology.md`),
not invented. These are the product.

- **P-A One stream, not many buckets.** Exactly one place to write.
- **P-B Classify by marking, not by filing.** Structure is added inline, after
  the thought, never before it.
- **P-C Views show only what was marked.** No automatic surfacing of unmarked
  content.
- **P-D Intent is declared, and capped.** A limit, not a ranking.
- **P-E The day closes with an audit, not homework.** Verify the fields; never
  ask a reflective question.
- **P-F Never collect what will not be used.**

## What the app refuses

1. **No settings screen for structure.** No folders, no vault picker, no
   user-editable templates, no plugin API. Appearance and keybindings may be
   adjustable; the shape of the system is not.
2. **No aspirational capture.** The app will not ask reflective questions or
   provide buckets for material filed against a future self who will process it.
   Logs are fine; homework is not.
3. **No feature that cannot be defended as a default.** If the honest answer to
   a request is "make it configurable", the answer is no.

Explicitly rejected during F2: **basic / intermediate / advanced modes.** That is
a settings screen with a better name — it still puts a decision in front of the
user before their first note, and it forfeits the only differentiation the
product has. Progressive disclosure decided *by the app*, based on observed use,
remains open for F3.

## The first 90 seconds

> The app opens directly on today's journal. It is quiet and uncluttered. No
> onboarding wizard, no vault picker, no folder chooser. The cursor is already
> where the user should type. Within 90 seconds the user has written about their
> day and made **zero** structural decisions.

Any feature that adds a decision to this minute is rejected on sight.

## Scope: a wide vision, a narrow first release

The maintainer deliberately held back every other part of his PKM until the
journal stabilised, then began looking outward. That sequence is not an accident
of scheduling — it is the adoption path, discovered in practice, and the product
follows it.

| | Pillar | Status | Evidence |
|---|---|---|---|
| 1 | **Opinionated work journal** | **MVP** | two years of iteration; two months of sustained higher productivity |
| 2 | Zettelkasten that is easy to learn and shows value early | vision | `[ASSUMPTION]` — previously used and dropped |
| 3 | Spaced repetition via simple in-note notation | vision | `[ASSUMPTION]` — never used by the maintainer |
| 4 | Personal OKRs / goals with simple notation | vision | `[ASSUMPTION]` — previously used and dropped |

**Only pillar 1 enters the MVP.** Pillars 2-4 are coherent with the thesis —
each is a case of taking a method that normally demands heavy setup and shipping
a working default — but none has evidence yet, and scope ambition is the
documented failure mode of this category (`competitive-analysis.md`: a funded
team lost years to it).

**Constraint on pillars 2-4:** each must be designed so the journal user
discovers it *without being sent to configure anything*. If a pillar needs a
setup step, it is not ready.

**The link between pillars is deliberately loose.** The journal does not
automatically feed permanent notes; a connection may exist but is not the
mechanism. This is a decision, not an omission — automatic promotion of fleeting
notes to permanent ones is exactly the aspirational machinery refusal 2 rejects.

## Non-goals for the MVP

- Mobile, sync, collaboration, web version, plugin ecosystem.
- Natural-language querying of notes (O3): real demand, crowded quadrant, and
  conflicts with offline-first.
- **Importing existing graphs.** Retained as a non-goal but now
  **under review in F3**: two independent bodies of evidence oppose "start
  clean" (H3), and the recurring counter-proposal is to archive rather than
  delete. A read-only path to the old vault is the likely hedge.

## An unvalidated claim worth testing

The maintainer observes that PKM tools lack dashboards that deliver real value.
This is plausible and matches P-C, but it is `[ASSUMPTION]`. Note that gen 1 of
his own template carried four automated views and he deleted all of them — the
lesson there was that generated views are noise unless the user marked the
content. Any dashboard must be built from marks, not from inference.

## How we will know it worked

The user still uses the app in month six. Metrics in `success-metrics.md`.