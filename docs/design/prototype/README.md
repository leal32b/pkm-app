---
status: reference
date: 2026-08-22
version: 1.0
phase: F3.3
source: docs/design/taxonomy.md, docs/design/main-flow.md
---

# Prototype — v0.1 visual reference

Static mockups produced in Claude Design over five iterations. **Visual
reference only**: no code from the prototype is reused, because it renders
fixed content with no state and the product is built in SolidJS on Tauri.

## What these images are authoritative for
Proportion, weight, rhythm, and the relative quiet of each element — things
prose cannot pin down.

## What they are NOT authoritative for
Behaviour, rules and vocabulary. **`taxonomy.md` and `main-flow.md` win over
these images in every conflict.** The prototype was a means of finding gaps in
those documents, not a specification in its own right.

## Known divergences from the final spec
- The images show `[[note]]` with a link treatment. In v0.1 it is a **mark, not
  a link**: no underline, no pointer cursor (`mvp-spec.md`).
- The images show a priority suffix (`· important`). Priority is **deferred to
  v0.2**.

## What the prototype found
Four gaps in the model, fixed in the documents before any code was written:
one-level hierarchy, separate visual channels per axis, the narrowed check-out
scope, and `waiting` without a person as a valid temporary state.

`brief.md` holds the final brief that produced these screens.