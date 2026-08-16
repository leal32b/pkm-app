---
status: draft
date: 2026-08-16
version: 0.1
phase: F2
source: docs/discovery/opportunity-map.md
resolves: tension T1
---

# Ideal customer profile

## Decision

The audience is **not** "non-technical people". That framing was an untested
assumption at project start and found no support in F1: the documented pains
come from experienced users. Tension T1 is resolved in favour of a narrower,
reachable group.

## Who

**People who already run a PKM system and are quietly losing to it.**

- Months or years on Obsidian, Logseq, Notion or Roam.
- Have rebuilt their setup at least once, often more.
- Comfortable with markdown and local files — not put off by an app that owns
  its own data format either.
- Currently in decline of use, or feel guilt about their system.
- Value privacy and local data enough that a cloud-only tool is a non-starter.

**Sharpest sub-segment:** users of file-based Logseq, whose product entered
maintenance-only mode when Logseq split into two versions. They have an active,
external reason to be looking, and they already accepted an opinionated tool.

## Who this is explicitly not for

- PKM beginners with no prior system. They have no pain to relieve yet, and no
  basis for comparison.
- Users who want to build a system. The refusals in `vision.md` are hostile to
  them, deliberately.
- Teams, collaboration, shared knowledge bases.

## The uncomfortable part

This audience is **the most configuration-fluent group that exists**. The
product's core proposition is to take configuration away from exactly the people
best equipped to use it. That is tension T3, and it is the central risk of the
strategy — not a detail. It is addressed in `hypotheses-and-risks.md` (F2.2).

Counter-argument, and the reason to proceed: the maintainer is a member of this
audience, resisted Logseq's imposed constraints, adapted, and concluded the
constraints were right (self-interview E5). One data point, not proof.

## Reachability

This group congregates in identifiable public places (PKM forums, subreddits,
Hacker News, the Logseq and Obsidian communities). That matters more than size
for a solo open-source project: it makes the first users findable without a
marketing budget.