---
status: accepted
date: 2026-08-22
version: 1.0
phase: F3
source: docs/design/taxonomy.md, docs/product/vision.md
constrains: F3.3 (prototype)
---

# Main flow

The MVP's only flow, written as the brief for the prototype. Five moments in a
day. Everything the product does in v0.1 happens here.

## Moment 1 — Open (morning)

The app opens directly on today's journal. Cursor ready. No vault picker, no
folder chooser, no onboarding, no first-run question of any kind (ADR 0003).

If the previous day was left unfinished, there is **one** discreet indicator —
not a screen, not a modal, not a list of what is missing. The unfinished day is
reachable in one action and is never forced.

> **Constraint:** yesterday's debt must never be the first thing the user has
> to deal with. That mechanism is the documented cause of abandonment (O2.1).

## Moment 2 — Declare intent

**Focus: one to three references to tasks.** Focus does not hold free text of
its own — it points at real tasks. A task may come from any day; carrying
yesterday's task into today's focus is the normal case.

Typing new text into a focus slot **creates that task in today's log** and
references it. The task lives in the log, which remains the only place to write
(P-A). Marking it done anywhere marks it done everywhere, because there is one
object.

**Intention: one open line of free text.** Deliberately not a task and not
linked to anything — it is a stance for the day, not an item of work.

Both are skippable. A skipped intent is not an error and produces no nagging.
The cap of three is the opinion (P-D): a limit, not a target.

## Moment 3 — Write (all day)

A single stream. This is where the user spends the day.

- Most blocks are **plain text with no marks**. This is the expected case.
- A block can be given a type, made a task, or made to reference a person or
  note — always **after** the sentence exists, never before (P-B).
- Marking must not require leaving the keyboard or breaking the flow of writing.

> **Constraint:** nothing in this moment may ask "where does this go?".

## Moment 4 — Collect (any time)

A view of **what was marked today**, grouped by type. Nothing else appears —
unmarked content is never surfaced (P-C).

Minimal by design in v0.1. This is the seed of the dashboards the maintainer
finds missing in other tools, and it is **the first thing cut if the appetite
runs short** in F3.5.

## Moment 5 — Close (end of day)

The check-out audit. Four verifications of the day's own fields:

1. **Focus** — derived, not asked. The linked tasks show their own state; if
   they are done, the check is met. The app never asks a question it can answer
   from what the user already marked (P-C).
2. Intention reached?
3. **Incomplete tasks** — tasks with no state, and `waiting` tasks with no
   person. Fixable in place; **each item disappears as it is resolved.**
4. Everything captured? — a question, answered in the log.

> **Scope of check 3 is deliberately narrow: it lists only blocks that are
> already tasks and are incomplete.** It must never ask the user to classify
> unmarked blocks. Most of the day is plain text written unmarked on purpose;
> demanding classification at day's end is aspirational capture in a new costume
> (refusal 2) and is precisely what the maintainer cut from his own template (C3).

A day with nothing pending shows check 3 empty and closes in silence. The
check-out is a list that empties, not a form to fill.

**Not optional.** The audit is the instrument behind the "days finished ≥ 80%"
metric (`success-metrics.md`).

## What this flow does not contain

No folder choice, no template selection, no save location, no reflective
prompts, no wizard, no settings screen for structure, no import.

## Resolved by the prototype (F3.3)

- **Type and task state occupy distinct visual channels** — see
  `taxonomy.md`, "Visual channels".
- **Marks live outside the sentence.** A marked block's text is byte-identical
  to a plain one's.
- **Check-out is appended to Today, not a separate screen.** The day's fields
  cannot be verified from somewhere the fields are not.
- **Timestamps: recorded always, displayed always, editable, not removable.**
- **No persistent shortcut cheatsheet.** A permanent cheatsheet is an admission
  that the interaction is not discoverable. Shortcuts surface while marking and
  never sit still on the screen.
- **No explanatory copy inside the UI.** A section that needs a caption is a
  section that is badly designed.
- **The fourth check ("everything captured?") is a question, not a field.** It
  returns the cursor to the activity log. A text box there would create a second
  place to write, breaking P-A.

## Still open

- Visual weight of the check-out section relative to the day above it.
- How an edited timestamp is entered without opening a dialog.