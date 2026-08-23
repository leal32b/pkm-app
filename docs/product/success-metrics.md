---
status: accepted
date: 2026-08-22
version: 1.0
phase: F2 (closing artifact)
source: docs/product/vision.md, docs/discovery/opportunity-map.md
---

# Success metrics

## The outcome

**The user still uses the app in month six.**

Every pain in F1 ends in abandonment, not in switching to something better. So
retention over months is the only outcome that proves the problem was solved.
Downloads, stars and installs are explicitly **not** success — they measure
curiosity, which this category generates easily and converts poorly.

## The measurement problem, stated honestly

A local-first desktop app with no telemetry and no accounts produces **no data
by default**. That is a deliberate consequence of the offline-first principle
(T2), not an oversight. Three constraints follow:

1. Nothing is measured without explicit opt-in (F7 decision, not MVP).
2. At MVP there is realistically **one user: the maintainer**. Any metric that
   needs a population is theatre until there is a population.
3. Therefore the MVP's primary instrument is **the maintainer's own sustained
   use**, measured the same way the current Logseq template was evaluated:
   did the days get finished, and did use decline.

This is weak evidence. It is also the only evidence available before shipping,
and pretending otherwise would produce dashboards measuring nothing.

## Tier 1 — MVP (n=1, self-observed)

The bar to declare the MVP a success. All three must hold.

| Metric | Target | How |
|---|---|---|
| **Migration completed** | maintainer stops opening Logseq for daily work | self-observed, binary |
| **Days finished** | ≥ 80% of workdays closed via the check-out audit | counted in-app; the audit already exists in the design |
| **No decline** | days used in week 12 ≥ days used in week 1 | counted in-app |

**Days finished** is the key one: it is O2.1 measured directly. Guilt-driven
abandonment shows up here first, weeks before the user stops opening the app.

**Falsification is the point.** If the maintainer drifts back to Logseq, or the
completion rate falls below the current template's, the product has failed on
its own terms and must be reshaped — not shipped harder.

## Tier 2 — Post-launch, without telemetry

Once released, before any telemetry exists (F6-F7):

| Signal | What it indicates | Source |
|---|---|---|
| Users reporting **week 4+ of continuous use** | retention, the actual outcome | unsolicited issues, discussions, posts |
| Requests for the **refused** features (settings, plugins, templates) | H1 failing in the wild | issue tracker, unprompted |
| Requests for **pillars 2-4** (Zettelkasten, spaced repetition, goals) | the journal stabilised and users are looking outward — the adoption path holding | issue tracker |
| **Silence after installation** | the 90-second test failing | absence of any of the above |

**The most valuable single signal** is the ratio between the second and third
rows. Requests to restore configuration mean the thesis is wrong. Requests for
the next pillar mean it is working and the sequence is right.

## Tier 3 — With opt-in telemetry (F7, not before)

Designed here only to constrain what may ever be collected, per P-F (*never
collect what will not be used*). Anything not on this list must not be built.

- Days finished per week (the same metric as Tier 1, aggregated).
- Week-over-week retention.
- Which marks are actually used, and which are never used — a mark nobody uses
  is a wrong default and should be removed, not documented.

**Never collected:** note content, titles, tags, counts of notes, or anything
from which content could be reconstructed. Opt-in, off by default, revocable,
and the collected payload must be inspectable by the user.

## Anti-metrics

Explicitly not tracked, and not to be celebrated:

- GitHub stars, downloads, install counts.
- Notes written per day. Rewarding volume contradicts refusal 2 (no aspirational
  capture) — a user writing less and finishing more is a success, not a decline.
- Session length. Longer sessions in this product mean the ritual grew heavy,
  which is the failure the product exists to prevent.

## F2 gate

Met: vision, ICP, hypotheses with risks, and metrics — with H1 tested as far as
available means allow and its weakened state recorded rather than smoothed over.

**Carried into F3 as open:** H1 remains an explicit bet; H3 ("start clean") is
probably wrong and must be reversed or hedged; the three tag vocabularies must
be reconciled into one.