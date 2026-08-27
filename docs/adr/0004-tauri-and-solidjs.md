---
status: accepted
date: 2026-08-22
version: 1.0
type: retroactive
related: docs/product/vision.md, docs/design/platform-support.md,
         docs/product/hypotheses-and-risks.md
---

# 4. Use Tauri with a SolidJS frontend

## Context

The stack was chosen before this decision log existed. It is recorded here
retroactively so the trade-offs are explicit and revisiting it later is a
deliberate act rather than a drift.

Constraints in play:
- **Lightness and performance are non-negotiable** and, per F1 research, a
  competitive position rather than a preference: performance degradation is the
  most documented complaint across the category after sync.
- **Offline-first**, no network required.
- **Solo maintainer, 7-14h/week, zero Rust experience.**
- Frontend experience: TypeScript, Node, SolidJS.

## Alternatives considered

**Electron.** Largest ecosystem, one rendering engine everywhere, and the
maintainer could be productive immediately. Rejected on the product's central
constraint: bundle size and memory are an order of magnitude worse, and the
category's loudest complaint is exactly that. Shipping a heavy app while
promising lightness would fail on its own terms.

**Native (SwiftUI).** Best possible performance and platform fit on the primary
target. Rejected: it forecloses Windows and Linux entirely, and the maintainer
has no Swift experience — trading one learning curve for another with less reuse.

**Wails (Go).** Same system-webview model as Tauri with a gentler language.
Rejected on ecosystem maturity and community size; Tauri's documentation,
plugins and permission model are further along.

**Web app.** Rejected by the vision: offline-first and local data are the point.

## Decision

**Tauri v2** (pinned to the 2.11.x line) with a Rust core and a **SolidJS +
TypeScript** frontend.

The exact patch version is pinned at scaffold time and recorded in `CLAUDE.md`.
Tauri's API changed significantly across majors, so any claim about its APIs,
plugins or configuration must be verified against the docs for the pinned
version rather than from memory.

## Consequences

**Accepted benefits**
- Small bundles and low memory, consistent with the product's core promise.
- An explicit capability/permission model, which becomes part of the threat
  model rather than configuration.
- Frontend built in a stack the maintainer already knows, so the learning curve
  is confined to the core.

**Accepted costs**
- **Three rendering engines, one verified.** Tauri renders through the system
  webview: WKWebView, WebView2, WebKitGTK. The maintainer can only launch the
  app on macOS (`platform-support.md`), so Windows and Linux rendering is
  unverified by construction. The macOS system WebKit — which updates only with
  the OS — sets the CSS and JS baseline for the whole product.
- **The Rust learning curve is unmeasured.** Hypothesis H5 has never been
  tested. The MVP estimate should be read as unverified until the walking
  skeleton ships.
- Smaller ecosystem than Electron: some problems will have no ready answer.

- **Most Rust will be written by an AI agent, not by the maintainer.** At
  7-14h/week with no Rust background, delegating the core to Claude Code is the
  realistic path. This does not remove the risk in H5, it moves it: the question
  becomes whether the maintainer can **review** Rust he did not write.

  That question matters more than the first one. He is the only reviewer, so
  unreviewed code is unapproved code; he cannot debug at 23:00 what he cannot
  read; and this is an app holding other people's personal notes, where a
  persistence bug he cannot follow is somebody else's data loss.

  **This is the strongest argument for the thin core** (ADR 0005): less Rust
  means less code the maintainer must be able to read. It also sets a rule —
  **no Rust is merged that the maintainer cannot explain line by line.** If an
  agent produces code he cannot follow, the response is to simplify it, not to
  merge it.

**Mitigations**
- **Keep the core thin** for the MVP: persistence and file I/O in Rust,
  everything else in the frontend. The boundary is fixed in ADR 0005 (F4.2),
  because moving it later is a rewrite.
- Keep the design inside the common subset of all three engines. The product is
  quiet and typographic, which makes this cheap.
- Verify Tauri API details against the docs for the pinned version rather than
  from memory — the API changed significantly across majors.

## Revision triggers

Any of these makes this ADR worth reopening. None of them is "Rust was hard on
a given day".

1. **Three consecutive weeks with no working increment**, blocked on the core.
   This tests H5 directly. Note that the test is not "could the maintainer write
   it" but "could he understand and review what was written for him" — code
   merged without comprehension is not progress, and this trigger should fire on
   that too. The first response is to thin the core further, not to change
   framework.
2. **A webview divergence produces a bug that cannot be fixed from macOS** and
   that affects the primary platform's users.
3. **A capability the product needs requires substantial Rust** beyond the thin
   core — for example a custom editor engine or heavy indexing.
4. **Tauri v2 stalls** (no releases, unanswered security issues) the way Logseq's
   rewrite did.

If trigger 1 fires, the honest alternative is Electron, accepting the weight
cost and revisiting the lightness promise in `vision.md` — not pretending both
can hold.