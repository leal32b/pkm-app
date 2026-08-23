---
status: accepted
date: 2026-08-22
version: 1.0
phase: F3 (closing artifact)
source: docs/product/vision.md, docs/design/taxonomy.md, docs/design/main-flow.md,
        docs/design/platform-support.md
---

# MVP spec — v0.1

## Appetite

**8 weeks.** Fixed. Scope gives, the date does not.

Maintainer's real pace is 1-2h on weekdays and 2-4h at weekends — roughly
7-14h/week, so **56-112 hours**, call it ~85. The maintainer has **zero Rust**
experience, and H5 (that Rust is learnable at this pace) has never been tested.
The estimate below should be read as unverified until the walking skeleton ships.

## Success condition

**The maintainer stops opening Logseq for daily work.** Nothing else counts.
Not a nice demo, not a clean codebase — a tool that replaced the incumbent for
its author.

## In scope

The complete daily loop: open → declare intent → write → mark → close the day.

1. **Journal stream** with one level of nesting.
2. **Four note types** — `decision`, `blocker`, `insight`, `question` — in the
   gutter, applied by command. *These are the product's opinion; without them
   this is an outliner with tasks, and Logseq does that better.*
3. **Task states** inline: `todo` / `waiting` / `done`.
4. **`@person`** — picker and inline reference. **No person page.**
5. **`[[note]]` as a mark, not a link.** The syntax is parsed and stored so that
   pages can be built in v0.2 with no data migration. Rendered quietly, with
   **no click affordance** — no underline, no pointer cursor. A link that opens
   nothing is a bug.
6. **Timestamps** on top-level blocks, recorded on first keystroke. **Not
   editable in v0.1.**
7. **Check-in**: focus (1-3) and intention. Typing in a focus slot creates the
   task in today's log. **No search across earlier days.**
8. **Check-out**: the four verifications; check 3 empties as items are resolved.
9. **Day navigation** plus the quiet indicator that yesterday was left open.
10. **Local persistence** in the OS application data directory.
11. **A macOS build downloadable from GitHub Releases.**

## Out of scope, and where it goes

| Deferred | To | Why |
|---|---|---|
| `[[note]]` pages with backlinks | v0.2 | A second surface with its own navigation and rendering — likely half the budget on its own. The mark ships now so no migration is needed later. |
| Moment 4 — "what I marked today" | v0.2 | Already flagged in `main-flow.md` as the first cut if the appetite ran short. It did. |
| Priority suffix (`important` / `urgent`) | v0.2 | The only item that can be faked by writing it in the sentence. |
| Focus referencing tasks from earlier days | v0.2 | Needs a cross-day task index — infrastructure, not a feature. |
| Editable timestamps | v0.2 | |
| Windows and Linux bundles | v0.2 | Best-effort tier; unverifiable by the maintainer (`platform-support.md`). |
| Auto-updater | v0.2 | Requires a key pair and a manifest endpoint — real F4 work. |
| **Code signing and notarisation** | **before any public announcement** | See below. |

### On shipping unsigned

v0.1 is unsigned and un-notarised, by decision. macOS Gatekeeper will block an
unsigned app downloaded from the internet, and the user must take a manual step
that is not obvious.

Acceptable for the maintainer and a handful of deliberate early users. **Not
acceptable for the F6 gate** — "installable by a stranger without the
maintainer's help" cannot be met unsigned. The Apple Developer account
(USD 99/year) must be acquired before any public announcement, not on the eve
of it.

## If the appetite runs out

Cut in this order, and record which cuts were made:

1. One level of nesting → flat stream
2. Check-in (focus and intention)
3. Two of the four types, keeping `decision` and `blocker`

**Never cut:** the four types entirely, the check-out, or local persistence.
Without the types there is no opinion; without the check-out the success metric
cannot be measured; without persistence there is no product.

## What v0.1 deliberately is not

No settings screen, no plugins, no folder picker, no import, no sync, no mobile,
no AI, no note pages, no dashboards. Refusals from `vision.md` hold in full.

## F3 gate

Met: taxonomy, main flow, prototype, platform support and a scoped spec with a
fixed appetite. Ready for architecture (F4).