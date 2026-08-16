---
status: living
date: 2026-08-16
version: 1.0
---

# Progress

Single source of truth for project state. Update at the end of every session.
Read this first when resuming work.

## Current phase

**F0 — Foundation** (repo and process setup). Nearly complete.

## Phase map

| Phase | Focus | State |
|---|---|---|
| F0 | Repo and process foundation | in progress |
| F1 | Discovery and problem framing | not started |
| F2 | Product strategy | not started |
| F3 | Solution design | not started |
| F4 | Architecture | not started |
| F5 | MVP construction | not started |
| F6 | Distribution and launch | not started |
| F7 | Continuous loop | not started |

## Decisions taken

| ADR | Decision | Date |
|---|---|---|
| [0001](adr/0001-record-architecture-decisions.md) | Record all decisions as ADRs | 2026-08-16 |
| [0002](adr/0002-license-agpl-3-0.md) | AGPL-3.0-or-later + DCO, no CLA | 2026-08-16 |

Decided but not yet recorded as ADRs (pending, F4):
- Tauri as the desktop framework (retroactive ADR, with trade-offs and revisit triggers)
- SolidJS as the frontend framework
- Closed scope: no third-party plugin ecosystem

## Open questions

- Product name (deferred to F2/F3; `pkm-app` is a working title).
- Discovery method: maintainer has no guaranteed access to interviewees, so F1
  will rely on secondary research (forums, issue trackers, reviews) plus
  disciplined auto-ethnography of the maintainer's own Logseq usage.
- Apple Developer account (USD 99/year) is required for notarization even when
  distributing outside the App Store. Not yet acquired. Blocking for F6.
- Tension to resolve in F1: "for non-technical people" and "offline-first local
  files" pull in opposite directions. The real ICP is undecided. `[ASSUMPTION]`

## Next step

Finish F0 by committing README, CLAUDE.md, PROGRESS.md and the two ADRs,
then start F1 (discovery).

## Session log

| Date | Phase | What happened |
|---|---|---|
| 2026-08-16 | F0 | Phase map approved. License decided (AGPL-3.0 + DCO). Public repo created. |