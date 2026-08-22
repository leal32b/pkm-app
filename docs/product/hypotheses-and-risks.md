---
status: draft
date: 2026-08-16
version: 0.1
phase: F2
source: docs/product/vision.md, docs/product/icp.md, docs/discovery/opportunity-map.md
resolves: tension T2
addresses: tension T3
---

# Hypotheses, risks and experiments

Every belief this strategy rests on, stated so it can be proven wrong cheaply.
Each experiment fits one session (≤2h) and none requires the product to exist.

## H1 — The configuration-fluent will accept losing configuration `[tension T3]`

> Experienced PKM users, tired of their own setup, will prefer a tool that
> decides for them over one they can shape.

**Why it is doubtful.** This is the group best equipped to configure and most
attached to doing so. The maintainer is n=1 and is also the author.
**If false:** the entire strategy is wrong and no amount of good execution
saves it. **Test first.**

- **E1 — Public position statement.** Post the refusals from `vision.md` — no
  settings for structure, no plugins, no user templates — in one PKM community,
  framed as a question, with no product, no repo link, no promise. Read the
  disagreement, not the agreement.
- **Signal of support:** several unprompted replies describing their own
  abandoned setup and saying they would try it.
- **Signal of failure:** the dominant reply is "just use X with fewer plugins",
  or the objections are all requests for the settings you refused.
- **Effort:** 1h to write, ~1 week to read replies.

## H2 — Guilt, not features, ends usage

> The trigger for abandonment is the feeling of being behind, not a missing
> capability.

**If false:** the product should compete on capability, and it will lose.

- **E2 — Ask the abandoners.** In the same or an adjacent community, ask people
  who stopped using their PKM what the *last* week of use felt like. Do not ask
  what was missing.
- **Signal:** answers describe overhead, backlog and guilt rather than gaps.
- **Effort:** 30 min to post, passive thereafter.

## H3 — A clean start is acceptable

> The target audience will try a tool that does not import their existing graph.

**Adopted as a decision** (`vision.md` non-goals) but unproven, and potentially
fatal: this audience has years of notes.
**Mitigating argument:** the product is for people whose current system already
failed them; carrying that system in may carry the failure in too.

- **E3 — Fold into E1.** State explicitly that there is no import and see whether
  it is the first objection raised.
- **Signal of failure:** import is the loudest objection, or people say they
  would only try it as a second, parallel tool.

## H4 — "Capture less" is the answer to O2.2

> Users who capture less will read back more, and feel better about the system.

With O3 out of scope, only two strategies remain for O2.2: **capture less** or
**resurface automatically**. This hypothesis picks the first.

- **E4 — Self-experiment, 2 weeks.** The maintainer strips his own Logseq daily
  template to the narrowest schema he can tolerate (the meeting schema from
  self-interview E3 is the model: relevant item, person, mine/waiting).
  Record daily: did the day get finished, and was anything read back.
- **Signal:** completed days go up. Note honestly if the answer is "no
  difference" — that points to *resurface* instead, and reshapes F3.
- **Effort:** 15 min setup, 2 min/day, 2 weeks. Start now; it runs in parallel.

## H5 — Rust is learnable at this pace `[technical]`

> A maintainer with zero Rust, at 5-10h/week, can ship a Tauri app.

**If false:** the timeline is fiction and the core must be even thinner.
Cannot be tested by discussion — only by building.

- **E5 — Deferred to F5's walking skeleton**, which doubles as this test. Flagged
  here so the F5 estimate is treated as unverified until the skeleton ships.

## Decision — tension T2, offline-first vs LLM `[RESOLVED]`

**Principle adopted:** *the app is fully functional with no network connection,
and no note content leaves the device without an explicit, per-action user
decision.*

This does not ban intelligent retrieval (O3) later; it constrains its shape.
Any future implementation must be local, or opt-in per action with the data
sent made visible. Recorded so that a future feature cannot erode offline-first
by accident, one convenience at a time.

To be re-recorded as a formal ADR in F4, where it becomes an architectural
constraint rather than a product principle.

## Risk register

| # | Risk | Impact | Mitigation |
|---|---|---|---|
| R1 | H1 is false — the audience wants control | fatal | E1 before any code |
| R2 | Solo maintainer burns out or stalls; project dies quietly | high | fixed appetite per cycle (F3); ship something installable early |
| R3 | Core rewrite becomes necessary (the Logseq failure mode) | fatal | data model decided deliberately in F4; no core rewrite, ever |
| R4 | Contributors arrive wanting the settings the product refuses | medium | refusals stated publicly in README and CLAUDE.md from day one |
| R5 | macOS notarization cost/bureaucracy discovered late | medium | Apple Developer account acquired during F4, not F6 |
| R6 | Scope grows past what one person can maintain | high | every new feature must be defensible as a default (vision, refusal 3) |
| R7 | Target audience responds to friction by building their own tool or wiring an LLM to the notes folder, rather than adopting someone else's product | high | the product must be better than a weekend hack, not just better than Obsidian |

## What must happen before F3

E1 and E2 posted. E4 started. F3 does not open on the strength of one person's
intuition — that is the honest gap left by F1.