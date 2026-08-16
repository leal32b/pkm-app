---
status: living
date: 2026-08-16
version: 1.1
---

# Progress

Single source of truth for project state. Update at the end of every session.
Read this first when resuming work.

## Current phase

**F1 — Discovery and problem framing.** Step F1.1 (self-interview) complete;
next is F1.2 (secondary research to corroborate the candidate pains).

## Phase map

| Phase | Focus | State |
|---|---|---|
| F0 | Repo and process foundation | **done** (2026-08-16) |
| F1 | Discovery and problem framing | **done** (2026-08-16) |
| F2 | Product strategy | in progress |
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

Process artifacts:
- `docs/internal/copilot-prompt.md` — the master prompt that drives the
  copilot sessions. Written in pt-BR (see `docs/internal/README.md`).
  Versioned so that session context is reproducible from the repo alone.

Decided but not yet recorded as ADRs (pending, F4):
- Tauri as the desktop framework (retroactive ADR, with trade-offs and revisit triggers)
- SolidJS as the frontend framework
- Closed scope: no third-party plugin ecosystem

## Open questions

Carried from F0:
- Product name (deferred to F2/F3; `pkm-app` is a working title).
- Apple Developer account (USD 99/year) is required for notarization even when
  distributing outside the App Store. Not yet acquired. Blocking for F6.

Raised in F1.1 (see [`docs/discovery/self-interview.md`](discovery/self-interview.md)):
- ~~T1 — ICP contradiction.~~ **Resolved 2026-08-16** in
  [`docs/product/icp.md`](product/icp.md): the audience is experienced PKM users
  in decline, not non-technical beginners.
- **T2 — Offline-first vs LLM.** Natural-language querying of one's own notes is
  the hottest signal, but a local model is heavy and a remote API breaks
  offline-first and note privacy. To be decided in F2/F4.
- **T3 — Opinionated vs power-user needs.** Graph-wide editing and periodic notes
  are normally answered with plugins or settings. Scope is closed (ADR 0002), so
  each must be answered with a default or refused outright. To be decided in F3.
- Discovery method: no guaranteed access to interviewees, so F1 relies on
  secondary research (forums, issue trackers, reviews) plus the self-interview.

## Current phase

**F2 — Product strategy.** F1 closed 2026-08-16; see
[`docs/discovery/opportunity-map.md`](discovery/opportunity-map.md).

## Next step

F2.2 — hypotheses, risks and cheap experiments, resolving tensions T2 and T3.
Output: `docs/product/hypotheses-and-risks.md`.

## Session log

| Date | Phase | What happened |
|---|---|---|
| 2026-08-16 | F0 | Phase map approved. License decided (AGPL-3.0 + DCO). Public repo created. |
| 2026-08-16 | F1 | F0 closed. Self-interview conducted; 7 candidate pains recorded; tensions T1-T3 opened. |
| 2026-08-16 | F1 | F1.2 done. P1/P2 strongly corroborated externally; P3 real but crowded; P4/P5/P7 dropped from MVP consideration. |
| 2026-08-16 | F1 | F1.2b done. Empty quadrant identified (open source + local-first + low setup). Logseq OG entered maintenance-only mode — displaced users are the initial audience candidate. |
| 2026-08-16 | F1 | F1.3 done. Opportunity map written; O1+O2 prioritised as the thesis, O3 held as an explicit bet. F1 gate met. |
| 2026-08-16 | F2 | F2.1 done. Vision and ICP drafted; T1 resolved. Three product refusals defined. O2.2 chosen as the first problem, constraining F3 to "capture less" and/or "resurface automatically". |