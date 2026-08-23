---
status: reference
date: 2026-08-22
version: 1.0
phase: F3.3
note: Consolidated from five iterations. This describes the screens as they
      ended up, not the sequence that got there.
---

# Prototype brief

Design an opinionated desktop journalling app. macOS primary. Light and dark.

## Thesis
This app ships a destination. Day one is where an experienced user arrived after
two years of trial and error with Obsidian and Logseq. It is deliberately
inflexible. Its value is that it has already decided.

## Who it is for
Someone who leads work and keeps a daily record of it — decisions, blockers,
open questions, and what they are waiting on from other people. They have used
Obsidian or Logseq for years and rebuilt their setup more times than they can
count. They are not impressed by software that looks impressive.

## Hard prohibitions
- No settings screen, gear icon, or preferences panel.
- No folder tree, vault picker, file browser, or sidebar of notes.
- No onboarding, wizard, or empty-state illustration.
- No template chooser, view switcher, or layout options.
- No reflective prompts anywhere.
- No badge counts, streaks, gamification, or progress rings.
- No AI features, chat panel, or assistant.
- No explanatory copy inside the UI. A section needing a caption is badly designed.
- No persistent shortcut cheatsheet — shortcuts surface while marking, never sit still.
- The user is never asked "where does this go?".

## Vocabulary — fixed
Four note types: `decision` · `blocker` · `insight` · `question`. A block has at
most one; most blocks have none.
Three task states: `todo` → `waiting` → `done`.
People are `@Name`, notes are `[[Note name]]`. There are no tags.

## Layout — the Today screen

One continuous scroll, bracketed by two titled rules:

**Check-in** — title centred on the divider, section collapsible.
  `focus` — one to three references to real tasks, rendered exactly as they
  appear in the log (same icon, same state word). Show one that came from an
  earlier day.
  `intention` — one open line of free text.

**Activity log** — the heart of the screen, visually dominant.

**Check-out** — title centred on the divider, section collapsible.
  `focus` — the same linked tasks, showing their current state. Derived, with
  nothing to tick.
  `intention` — `reached  not reached`.
  `incomplete` — only tasks with no state, or `waiting` with no person. Items
  disappear as they are resolved; an empty list reads "nothing left".
  `captured` — "Everything captured?" with a link back to the log. Not a field.

Section labels (`focus`, `intention`, `incomplete`, `captured`) are small
subtitles above their content, clearly lighter than body text.

## The three channels

**Gutter** — carries type marks and timestamps, and nothing else. Marks align to
the first line of their block, lower case, right-aligned. Timestamps sit between
the mark and the text. Only top-level blocks have a time; an empty block shows none.

**Text** — task state sits inline at the head of the line and takes only the width
it needs. Marked and unmarked lines share the same left edge. Icon plus word:
`ti-square-rounded` for `todo` and `waiting`, `ti-square-rounded-check` for
`done`; the word in small caps and bold, at body size, never larger. No chip,
no border, no category colour.

**Sentence** — people appear inline as `@Name`. A `waiting` block names its
person right after the state word when known.

## Nesting
Exactly one level. A block may have children; a child may not. Children are
bulleted and indented one step, carry no timestamp, and may have their own type,
state and people.

## Colour and weight
One hue, three weights: `blocker` is the only coloured mark, `decision` at full
contrast, `insight` and `question` muted. Someone scanning the day should feel
calm, not parsed.

## Tone
Quiet, dense with content, light on chrome — closer to Linear, iA Writer or a
well-set page than to Notion or a productivity dashboard. The user is writing,
not operating software.

## Content
Design the screen twice, with two content sets: a systems-and-code day and a
people-and-conversations day. Roughly a dozen blocks each, only four carrying a
type. If the marks visually dominate the plain text, the design has failed.