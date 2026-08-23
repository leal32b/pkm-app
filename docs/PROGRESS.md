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
| F2 | Product strategy | **done** (2026-08-22) |
| F3 | Solution design | in progress |
| F4 | Architecture | not started |
| F5 | MVP construction | not started |
| F6 | Distribution and launch | not started |
| F7 | Continuous loop | not started |

## Decisions taken

| ADR | Decision | Date |
|---|---|---|
| [0001](adr/0001-record-architecture-decisions.md) | Record all decisions as ADRs | 2026-08-16 |
| [0002](adr/0002-license-agpl-3-0.md) | AGPL-3.0-or-later + DCO, no CLA | 2026-08-16 |
| [0003](adr/0003-start-clean-no-import.md) | Start clean — no import of existing graphs | 2026-08-22 |
| [0004](adr/0004-tauri-and-solidjs.md) | Tauri v2 (2.11.x) + SolidJS, retroactive | 2026-08-22 |

Process artifacts:
- `docs/internal/copilot-prompt.md` — the master prompt that drives the
  copilot sessions. Written in pt-BR (see `docs/internal/README.md`).
  Versioned so that session context is reproducible from the repo alone.

Decided but not yet recorded as ADRs (pending, F4):
- Tauri as the desktop framework (retroactive ADR, with trade-offs and revisit triggers)
- SolidJS as the frontend framework
- Closed scope: no third-party plugin ecosystem

## Open questions

Live items only. Settled decisions move to the log below.

**Product**
- Product name. `pkm-app` is a working title; naming was deferred out of F2/F3.
- **H1 — will configuration-fluent users accept losing configuration?**
  The project's make-or-break assumption. E1 (public position post) could not be
  run; E1-alt (passive listening) **weakened** it — the audience solves this pain
  with self-discipline inside flexible tools and does not ask for imposed
  constraints. Now an explicit bet, not a premise.
- **`question` kill criterion.** If the type is not used at least weekly during
  the first two months of real use, it is removed from the product, not
  documented as underused (`taxonomy.md`).
- **Vocabulary revision trigger.** Recurring requests for a fifth concept become
  an ADR: either it ships as a new default, or the vocabulary opens. The decision
  must be explicit, never accidental (`taxonomy.md`).
- **ADR 0003 watch.** Whether the maintainer misses his Logseq history during the
  MVP. Archive (read-only access to the old vault) is the first response if so.

**Technical**
- **H5 — is Rust workable at this pace?** Reframed in ADR 0004: most Rust will be
  agent-written, so the real question is whether the maintainer can *review* it.
  Untested; the walking skeleton (F5) is the test.
- **Offline-first as an architectural constraint.** Adopted as a product
  principle in F2.2; still needs a formal ADR in F4.
- **Windows and Linux are compiled but never launched.** No machine available, so
  webview rendering there is unverified by construction. Declared best-effort
  (`platform-support.md`); closes only via an early user, a cheap machine, or
  screenshot tests in CI.

**Blocking F6**
- **Apple Developer account (USD 99/year)** for signing and notarisation. Not
  acquired. v0.1 ships unsigned by decision, which is acceptable for deliberate
  early users but **cannot meet the F6 gate** — "installable by a stranger" is
  impossible unsigned. Required before any public announcement.

## Settled

| Question | Outcome | Date |
|---|---|---|
| T1 — ICP contradiction | Experienced PKM users in decline, not non-technical beginners (`icp.md`) | 2026-08-22 |
| T2 — Offline-first vs LLM | Fully functional offline; no note content leaves the device without an explicit per-action decision (`hypotheses-and-risks.md`) | 2026-08-22 |
| T3 — Opinionated vs power users | Became hypothesis H1 (see above) | 2026-08-22 |
| H3 — is "start clean" acceptable? | Start clean, **against the evidence**, as a deliberate bet (ADR 0003) | 2026-08-22 |
| H4 — is "capture less" the answer to O2.2? | **Supported**: two months of sustained use with a narrower template, self-reported higher productivity. n=1, interested subject. | 2026-08-22 |
| Discovery method | No guaranteed access to interviewees; F1 ran on secondary research plus self-interview | 2026-08-22 |

## Current phase

**F3 — Solution design.** F3.1 to F3.3 complete. Next: F3.4 (OS conventions and
support matrix).

## Next step

F3.5 — MVP spec with a fixed appetite. Closes F3.

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
| 2026-08-22 | F1 | Market pain research incorporated (F1.2c). O4 upgraded to strong evidence — performance is a competitive position, not a preference. Three strategy conflicts recorded (sync, mobile, import). E1 cancelled; H1 remains untested. |
| 2026-08-22 | F2 | E1-alt run (passive listening, HN thread n=348 comments). H1 weakened — pain confirmed, solution shape not. H3 probably wrong. O2.2 re-scoped to aspirational capture. R7 added. |
| 2026-08-22 | F2 | Vision rewritten (v0.2): thesis moved from "no configuration" to "the destination". Six design principles adopted from template archaeology. Four-pillar vision recorded; MVP locked to pillar 1 (work journal). Tiered modes explicitly rejected. |
| 2026-08-22 | F2 | F2.3 done, F2 gate met. Success metrics defined around retention and finished days; anti-metrics recorded. Artifact dates corrected. |
| 2026-08-22 | F3 | F3.1 done. Taxonomy fixed: three axes, seven concepts (was nine in one flat list). `risco` and `aprendi` absorbed; priority demoted to attributes; `question` added with a kill criterion. UI language set to English, i18n deferred. |
| 2026-08-22 | F3 | F3.1 done. Taxonomy locked: three axes, seven concepts. `risco` and `aprendi` absorbed; priority demoted to attributes; free-form tags cut in favour of notes; `question` added with a kill criterion. Person syntax `@[[ ]]`. Revision trigger documented. |
| 2026-08-22 | F3 | F3.2 done. ADR 0003: start clean, no import — decided against the evidence, with revision triggers. Main flow defined in five moments; Moment 4 (collect) in MVP as minimal, first to cut. |
| 2026-08-22 | F3 | F3.3 prototyped in Claude Design. Prototype exposed a model flaw: type and task state had been collapsed into one channel, making a block unable to be both. Fixed in taxonomy — three axes, three channels. Timestamps decided. |
| 2026-08-22 | F3 | Second prototype iteration. Two model gaps found and closed: hierarchy (one level, was undefined) and check-out scope (was demanding classification of unmarked blocks — refusal 2 violation). Timestamps now recorded on first keystroke. |
| 2026-08-22 | F3 | F3.3 closed after five prototype iterations in Claude Design. Four model gaps found and fixed: one-level hierarchy, check-out scope, focus as task references, and `waiting` without a person as a valid temporary state closed at check-out. |
| 2026-08-22 | F3 | F3.4 done. Support tiers set (macOS primary; Windows 11 and Ubuntu LTS supported). WebView divergence documented — macOS WebKit sets the CSS/JS baseline. OS conventions kept deliberately shallow: native chrome, system fonts, OS-driven theme. |
| 2026-08-22 | F4 | F4.1 done. ADR 0004 records Tauri + SolidJS retroactively with alternatives and four revision triggers. H5 reframed: the risk is reviewing agent-written Rust, not writing it — hence the line-by-line review rule in CLAUDE.md. |