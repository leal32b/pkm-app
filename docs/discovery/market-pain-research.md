---
status: accepted
date: 2026-08-16
version: 1.0
phase: F1 (retroactive addition)
source: docs/internal/research/2026-08-pkm-user-pains-raw.md
affects: docs/discovery/opportunity-map.md, docs/product/vision.md, docs/product/hypotheses-and-risks.md
---

# Market pain research — synthesis

English synthesis of a broader pt-BR study covering 14 PKM tools, drawn from
official forums, GitHub issue trackers and aggregated review sites. Kept short
by design; the full material is the raw input linked above.

**Nature of the evidence.** Complaints from people who already use these tools.
It maps what is broken, not what people would adopt. It cannot confirm or
falsify H1, which remains untested.

## What it confirms

**O1 (setup as an endless project)** — corroborated with a name and a number.
"Shiny object syndrome" is a documented category-wide behaviour: optimising the
note system becomes a form of procrastination. Tana is criticised specifically
for requiring 3-5 hours of setup before the payoff, with users building half a
system and wrongly concluding the tool does not work. Steep learning curves are
tolerated *only when value arrives fast*.

**O4 (the app itself gets in the way)** — **upgraded from weak to strong.**
Performance degradation is the single most documented complaint after sync.
A Logseq user with ~2,000 pages reported ~4 minutes to open the app on an SSD
MacBook, and 10+ minutes on an older iMac. Obsidian's graph view degrades at
thousands of notes; Heptabase's whiteboards degrade at hundreds of cards;
AppFlowy shows reports of 5-10 minute startups and >90% CPU on tiny workspaces.

**Implication:** the "lightness" constraint is not a preference, it is a
competitive position. In this category the marquee feature is usually the first
thing to break at the scale users are told to aim for.

## What it adds

**N1 — Trust erosion outranks features.** Evernote's decline is attributed less
to any technical gap than to broken trust: a free tier cut from unlimited to 50
notes, retroactive mid-subscription price changes, a buried cancel button.
Roam's decline is attributed to price against free alternatives. **Directly
relevant to the paid-sync plan in ADR 0002:** whatever is promised free must
stay free, permanently and publicly.

**N2 — AI is read as a smokescreen.** Users of this category are technically
literate and react badly to AI features shipped while basic bugs persist
(Evernote, RemNote, Tana). Supports keeping O3 out of the MVP — for reputational
reasons, not just capacity ones.

**N3 — Search is rarely anyone's strength.** Across tools, search is described as
"good enough" rather than as a differentiator, despite retrieval being the
category's stated purpose. Possible unoccupied ground, adjacent to O2.2.

**N4 — Maintainer risk is a recognised anxiety.** Trilium's original maintainer
leaving caused real uncertainty before the community took over. A solo
open-source project holding someone's years of notes carries this by default.
Feeds risk R2; argues for a plain, boring, portable data format.

## Where it contradicts the current strategy

The research's own recommendations point at three things this project has
explicitly refused. Recording the disagreement rather than resolving it.

| Research says | Project decided | Assessment |
|---|---|---|
| Reliable sync is the largest differentiation opportunity in the category | Out of MVP scope; paid separate service later (ADR 0002) | **Not a conflict, a sequencing question.** Sync is where the money is *and* where every competitor breaks. Confirms the business model; the MVP is right to stay local-only. |
| Mobile should be first-class from day 1 — no tool has parity | Desktop only, no mobile | **Real conflict, accepted.** A solo maintainer at 5-10h/week cannot ship three desktop platforms and mobile. Note that this is a known, permanent weakness, not an oversight. |
| Robust importers reduce the cost of "one more try" | No import — "start clean" (`vision.md`) | **Real conflict, and evidence against H3.** This is the first external evidence bearing on that decision, and it points the wrong way. H3 is now *weakened*, not merely untested. |

**H3 needs revisiting in F3.** The strategic argument for a clean start (the old
system failed you; do not carry it in) still stands, but it is now a bet made
*against* available evidence rather than in the absence of it. One cheap hedge
exists: no import, but a *read-only* way to keep the old vault reachable. To be
argued in F3, not assumed now.

## What it does not do

It does not test H1. Every source here is a person complaining about a tool they
use. Nobody in this dataset was asked whether they would give up configuration,
because no such tool exists to complain about. The project's central assumption
remains unvalidated.