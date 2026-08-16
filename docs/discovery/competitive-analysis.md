---
status: accepted
date: 2026-08-16
version: 1.0
phase: F1
source: docs/discovery/self-interview.md, docs/discovery/secondary-research.md
method: secondary research on public sources, 2026-08-16
---

# Competitive analysis — where the gap is

**Scope.** Deliberately narrow. The question is not "what do all PKM tools do",
it is: *is there an unoccupied position for an opinionated, local-first,
open-source, low-setup desktop PKM?* Feature-by-feature comparison is out of
scope until there is a product to compare.

**Source warning.** Most PKM comparison content is vendor-authored: the Tana
blog ranks Tana first, the Storyflow blog ranks Storyflow first. Every claim
below is treated as marketing until corroborated. One widely repeated survey
statistic about canvas-based tools was found only on a vendor blog with no
retrievable primary source and is therefore **excluded**.

## The four paradigms (2026)

Public commentary converges on a four-way split, useful mainly as vocabulary:

| Paradigm | Tools | Unit of thought |
|---|---|---|
| Linked notes | Obsidian, Logseq, Roam | markdown file + backlinks |
| Object-based | Capacities, Anytype, Tana | typed object with properties |
| Visual canvas | Heptabase, Scrintal | card on a whiteboard |
| AI-native | Reflect, Mem | the query |

## The axis that actually matters here

Not paradigm — **setup cost**. Reported time-to-productive ranges from zero to
weeks. Notion and Obsidian are described as requiring users to build their own
system from scratch, potentially hours of template and plugin work. Tana and
Logseq are described as rewarding extensive setup but demanding it upfront.
Mem, Reflect and Capacities are described as working immediately or near it.

This is P1 restated by the market itself, and it is the axis this project bets on.

## The gap

Cross setup cost with licensing and data locality:

| | **High setup** | **Low setup** |
|---|---|---|
| **Closed / cloud** | Notion, Tana, Roam | Reflect, Mem, Capacities |
| **Open source / local-first** | Obsidian*, Logseq, Anytype | ← **empty** |

\* Obsidian is free and local-first but not open source.

Every tool that ships strong opinions and low setup is **closed source and
paid**. Every open-source local-first tool hands the user a blank canvas and a
configuration surface. Anytype is the nearest neighbour — open source,
local-first, E2E encrypted — but is repeatedly described as assuming the user
already understands object-based note-taking, i.e. it did not solve setup cost.

**This is the position.** `[ASSUMPTION]` The gap being empty does not prove it
is valuable; it may be empty because opinionated + open source is a
contradiction in practice (contributors arrive wanting settings). That risk
is now explicit and belongs in F2.

## The Logseq window

Logseq began a database rewrite around late 2022. As of April 2025 it had not
shipped, with roughly a year between releases, and community threads openly
questioning whether the project was alive. The team has since **split the
product in two**: "Logseq OG" (file-based) enters maintenance — security and
framework upgrades, **no new features** — while the database version becomes the
main product. Migration is not forced, and the two can be installed side by side.

**Reading.** A population of file-based Logseq users has just been told, politely,
that their app is done evolving, and is being asked to migrate to a product with
different tag and namespace semantics. That is an unusually large group of
people with an active reason to look around — including this project's
maintainer. It is also a warning: Logseq had funding and a team and still lost
years to a core rewrite. A solo maintainer at 5-10h/week cannot afford one, so
the data model decision in F4 carries more weight than usual.

**Second reading, uncomfortable:** they had money and people and still stalled.
Ambition is the failure mode in this category, not lack of features.

## Implications

1. The differentiator is not features. It is **what the product refuses to let
   you configure**. Every competitor's answer to a need is a setting or a plugin.
2. Obsidian's paid sync is repeatedly cited as the trigger that sends users
   looking for alternatives — supporting a paid-sync business model (ADR 0002)
   *and* warning that pricing it wrong reproduces the trigger.
3. Competing on AI-native retrieval (P3) means entering the most crowded
   quadrant, against funded teams. Competing on setup cost means entering an
   empty one. F2 must choose deliberately.
4. Do not attempt a core rewrite. Ever. Get the data model right in F4 or accept
   living with it.

## Sources

C1 liveit.me, "11 Best Second Brain Apps in 2026" (2026-04) — setup-cost claims ·
C2 buyersprint.com, "Best Obsidian Alternatives 2026" (2026-05) — four paradigms, sync-price trigger ·
C3 toolfinder.com, "Best Capacities Alternatives" (2026-05) — Anytype complexity ·
C4 solanky.dev / Medium, "Logseq Migration Journey" (2025-04) — rewrite timeline ·
C5 logseq.io announcement — the OG/DB product split ·
C6 tana.inc blog (2026-07) — vendor-authored, used only for paradigm vocabulary