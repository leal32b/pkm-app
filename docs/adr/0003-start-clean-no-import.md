---
status: accepted
date: 2026-08-22
version: 1.0
related: docs/product/vision.md, docs/discovery/market-pain-research.md,
         docs/discovery/experiments/e1-alt-passive-listening.md
---

# 3. Start clean — no import of existing graphs

## Context
The MVP targets people with years of notes in Obsidian, Logseq or Notion.
Whether to import them was left open as hypothesis H3.

**The available evidence opposes starting clean.** Market research reports that
robust importers lower the cost of "one more try" for a new tool. Independent
community discussion produced two unprompted arguments against discarding:
teams that declare a knowledge base a mess and start fresh end up maintaining
*two* bad knowledge bases; and people who deleted personal archives report
regret, with the recurring counter-proposal being to archive rather than delete.

Three options were considered:
1. **Import** — convert the old graph into the new taxonomy.
2. **Archive** — mount the old vault read-only and searchable, unconverted.
3. **Start clean** — no path to old content at all.

## Decision
**Start clean.** The MVP provides no import and no archive.

## Rationale
Import was rejected on product grounds: converting an old graph brings in the
free-form tags, templates and folder structures that constitute the system that
failed the user. Importing the old system imports the old problem, and
contradicts the product's thesis.

Archive was the recommended middle path and was **rejected by the maintainer**
in favour of the simpler option for the MVP, on the grounds that it can be added
later without breaking anything.

## Consequences
- **This decision is made against the available evidence, deliberately.** It is
  a bet, not a finding. Recorded as such so it is not later mistaken for a
  validated choice.
- Adoption friction is higher for the target audience. Some users will run the
  product as a second, parallel tool, or not try it at all.
- The MVP stays smaller, and the first-run experience keeps the 90-second test
  intact with no extra question.
- Adding an archive later is additive and breaks nothing, so the decision is
  reversible in the safe direction.

## Revision triggers
- The maintainer, as first user, misses access to his Logseq history during the
  MVP period.
- "No import" is the dominant objection raised by early users.
- Users report running the product alongside their old tool rather than
  replacing it.

If any trigger fires, the archive option (2) is the first response — not import.