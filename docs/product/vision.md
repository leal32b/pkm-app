---
status: draft
date: 2026-08-16
version: 0.1
phase: F2
source: docs/discovery/opportunity-map.md
---

# Product vision

## One line

**A knowledge app that has already made the decisions, so the only thing left
to do is write.**

## The bet

Every mainstream PKM tool answers a user need by adding a setting, a template or
a plugin. That is why setup is never finished and why the daily ritual grows
until it collapses (O1, O2). This project bets the opposite: **that a fixed,
well-chosen set of decisions beats an infinitely adjustable one**, for people who
have already lost that argument with their current tool.

## What the app refuses

These are prohibitions, not preferences. Each one closes a door that competitors
leave open, and each is the reason the app can stay small.

1. **No settings screen for structure.** No choosing where a note lives, no
   folders, no user-defined templates, no plugin API. Appearance and keybindings
   may be adjustable; the shape of the system is not.
2. **No unbounded capture.** The app will refuse to become a place to dump
   things that will never be read. Capture is narrow by design, and the app
   would rather you write less than write into a void.
3. **No feature the maintainer cannot defend as a default.** If the honest
   answer to a request is "make it configurable", the answer is no.

## Non-goals for the MVP

- Natural-language querying of your own notes (O3). Real demand, wrong quadrant,
  and it conflicts with offline-first. Deferred, argued in F2.2, not abandoned.
- Mobile, sync, collaboration, web version, plugin ecosystem.
- Migrating existing graphs from other tools. `[ASSUMPTION: users will start
  fresh — needs testing, this may be a hard blocker for the target audience.]`

## The first 90 seconds

The product's whole thesis has to survive its first minute, so it is specified
as a requirement rather than left to implementation:

> The app opens directly on today's journal. It is quiet and uncluttered. There
> is no onboarding wizard, no vault picker, no folder chooser, no empty-state
> illustration explaining what to do. The cursor is already where the user
> should type. Within 90 seconds the user has written about their day and made
> **zero** structural decisions.

Any feature that adds a decision to this minute is rejected on sight.

## The problem being solved first

O2.2 — *capturing things you know you will never read again.*

Chosen by the maintainer as the sharpest of the O2 cluster. It carries a hard
constraint: with O3 out of scope, the only remaining strategies are
**(a) capture less** and **(b) resurface automatically**. Both are product
design rather than technology, which suits a solo maintainer. F3 must pick one
or both explicitly.

## How we will know it worked

The user still uses the app in month six. Metrics in F2.3.