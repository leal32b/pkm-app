---
status: accepted
date: 2026-08-22
version: 1.0
related: docs/adr/0004-tauri-and-solidjs.md, docs/product/mvp-spec.md
constrains: F5
---

# 5. Core ↔ UI boundary

## Context

Tauri splits an application in two: a Rust core with full system access, and a
frontend running in an untrusted system webview. **Where the line falls is the
most expensive decision of this phase** — moving it later is a rewrite, and it
determines how much Rust the maintainer must be able to review (ADR 0004).

Two principles pull against each other:
- *Sensitive or heavy logic belongs in the core.*
- *Keep the core thin*, because the maintainer has no Rust and is the sole reviewer.

For v0.1 the tension resolves cleanly: **nothing is heavy yet** — a day's journal
is dozens of blocks, trivial for the frontend — and **only one thing is
sensitive: not corrupting the user's data.** That one thing goes in the core.

## Decision

### The core (Rust) owns
1. **All file I/O.** Nothing else touches the disk.
2. **Atomic writes.** Write to a temporary file, fsync, rename. A crash mid-save
   must never leave a partial or corrupt day.
3. **Where data lives** — the OS application data directory, resolved by Tauri.
   Never a user-chosen path (there is no vault picker).
4. **Format version and migrations** (ADR 0006).
5. **Reference extraction.** Given a day's text, return the people and notes it
   references. The core is the **authority** on what a reference is.

That is the whole list.

### The frontend (SolidJS) owns
The editor, all interaction and keyboard handling, gutter and mark rendering,
one-level nesting, timestamps at first keystroke, derived state (the check-out
list, focus state), and day navigation.

It also owns **syntax highlighting** — the live, per-keystroke recognition of
`@[[ ]]` and `[[ ]]` that drives the picker and the visual treatment.

### The contract
**Plain text on disk is the source of truth. Parsing is a display concern.**

The core hands the frontend the text of a day and writes back the text it is
given. It does not know what a `decision` is, what a task state means, or what
`@[[Ana]]` refers to.

```
load_day(date)              -> String
save_day(date, text)        -> ()
list_days()                 -> Vec<Date>
extract_references(text)    -> References { people, notes }
```

### Two parsing jobs, deliberately split

"Parsing" is two different jobs with different constraints, and they land on
different sides of the boundary.

| | Highlighting | Extraction |
|---|---|---|
| Runs | on every keystroke | on save, in batch |
| Purpose | show the picker, style the mark | answer "what does this day reference" |
| Lives in | **TypeScript** | **Rust** |

**Highlighting cannot live in Rust.** Every keystroke would cross the IPC
boundary into the webview. Even when fast, that is accumulated latency in the
most sensitive place in the product — typing — and lightness is the product's
central promise. An editor that lags fails faster than one missing features.

**Extraction must live in Rust.** It is batch work with no perceived latency,
it is testable, and it is precisely what v0.2 needs for backlinks and a task
index. Putting it in the core now means that debt is never incurred.

> **Rule when the two disagree: Rust wins.** Highlighting may miss a case
> visually; it must never determine what was referenced. There is one extractor,
> and it is in the core.

This is not two parsers in the harmful sense. It is a highlighter and an
extractor, with different responsibilities. Two *extractors* would be the harmful
case, and there is only one.

## Rationale

- **Minimum Rust.** Three commands and an atomic write is code the maintainer can
  read line by line, which is the review rule from ADR 0004.
- **Portability, which is a real risk mitigation.** A solo-maintainer app holding
  someone's personal notes must survive its maintainer (risk N4). Files that are
  greppable in a terminal do; a proprietary binary store does not.
- **The syntax is stored, so v0.2 needs no migration.** `[[note]]` ships as a
  mark in v0.1 (`mvp-spec.md`) and its text is already on disk when pages are
  built later.

## Consequences

**Accepted**
- **The core is larger than the minimum.** Three commands plus an atomic write
  would have been ~100 lines; adding the extractor with tests roughly doubles
  it. Still reviewable line by line (ADR 0004), but H5 remains untested and this
  is the first place it will be felt.
- **Whole-day granularity.** Saving rewrites the day's text. Fine at this size;
  revisit if a day ever becomes large enough for that to be felt.
- Loading many days at once means reading many files. Out of scope for v0.1,
  and the reason ADR 0006 must not make an index impossible later.

**Explicitly not in the frontend**
Any path construction, any direct disk access, any write that is not atomic.

## Saving

**Autosave, debounced ~1s after the user stops typing.** No save button, no
save shortcut, no "unsaved changes" state — the user is writing, not operating
software, and an unsaved journal is a lost journal.

Combined with atomic writes, frequent saves are safe: a crash costs at most the
last second of typing, never the file.

## Capabilities
Tauri permissions are granted at the minimum needed for the three commands
above, and are reviewed with every new feature. Permissions are part of the
threat model (F4.5), not configuration.

## Revision triggers

1. **A day's journal grows large enough that whole-file saves are noticeable.**
2. **Cross-day features arrive** (note pages, task index, search) and duplicating
   the parser in Rust becomes cheaper than indexing in the frontend.
3. **Data corruption is observed even once.** The core's single responsibility
   failed; that is a stop-everything event, not a bug in the queue.
4. **Typing latency becomes perceptible.** Measured in the walking skeleton
   before anything is built on top. If highlighting in TypeScript is not fast
   enough, the answer is a simpler highlighter — not moving it to Rust.