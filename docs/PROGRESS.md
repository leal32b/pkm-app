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
- ~~T2 — Offline-first vs LLM.~~ **Resolved 2026-08-16** in
  [`docs/product/hypotheses-and-risks.md`](product/hypotheses-and-risks.md):
  fully functional offline; no note content leaves the device without an
  explicit per-action decision. To become a formal ADR in F4.
- **H1 — will configuration-fluent users accept losing configuration?** The
  project's make-or-break assumption. Experiment E1 (public position post) was
  designed but **cannot be run by the maintainer**. Still untested; an
  alternative test must be designed before F5 commits significant build effort.
- **H3 — is "start clean" acceptable?** Weakened by market research: importers
  are reported to lower the cost of trying a new tool. Revisit in F3.
- Discovery method: no guaranteed access to interviewees, so F1 relies on
  secondary research (forums, issue trackers, reviews) plus the self-interview.

## Current phase

**F2 — Product strategy.** F1 closed 2026-08-16; see
[`docs/discovery/opportunity-map.md`](discovery/opportunity-map.md).

## Next step

F2.3 — success metrics. In parallel: run experiments E1, E2 and start E4.

## Session log

| Date | Phase | What happened |
|---|---|---|
| 2026-08-16 | F0 | Phase map approved. License decided (AGPL-3.0 + DCO). Public repo created. |
| 2026-08-16 | F1 | F0 closed. Self-interview conducted; 7 candidate pains recorded; tensions T1-T3 opened. |
| 2026-08-16 | F1 | F1.2 done. P1/P2 strongly corroborated externally; P3 real but crowded; P4/P5/P7 dropped from MVP consideration. |
| 2026-08-16 | F1 | F1.2b done. Empty quadrant identified (open source + local-first + low setup). Logseq OG entered maintenance-only mode — displaced users are the initial audience candidate. |
| 2026-08-16 | F1 | F1.3 done. Opportunity map written; O1+O2 prioritised as the thesis, O3 held as an explicit bet. F1 gate met. |
| 2026-08-16 | F2 | F2.1 done. Vision and ICP drafted; T1 resolved. Three product refusals defined. O2.2 chosen as the first problem, constraining F3 to "capture less" and/or "resurface automatically". |
| 2026-08-16 | F2 | F2.2 done. Five hypotheses and six risks recorded; T2 resolved by principle; T3 became hypothesis H1, to be tested before F3. |
| 2026-08-16 | F1 | Market pain research incorporated (F1.2c). O4 upgraded to strong evidence — performance is a competitive position, not a preference. Three strategy conflicts recorded (sync, mobile, import). E1 cancelled; H1 remains untested. |