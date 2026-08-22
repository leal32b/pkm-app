---
status: accepted
date: 2026-08-22
version: 1.0
phase: F3
source: docs/discovery/template-archaeology.md, docs/product/vision.md
constrains: F3.3 (prototype), F4 (data model)
---

# Taxonomy

The product's vocabulary. Because there is no plugin API and no user-editable
templates, **this list is the product's opinion**. Anything not here cannot be
expressed, by design.

## Language

The interface, the marks and all user-facing text are **English**. i18n is
deferred until there is a reason for it; shipping one language well beats
shipping two badly. Recorded as a product decision, distinct from the
repository's English-only rule in `CLAUDE.md`.

## Three axes, not one list

The maintainer's previous system had nine concepts because one mechanism
(inline tags) was carrying three different kinds of meaning. Separating them
shrinks each axis to something a person can hold in their head.

### Axis 1 — Note type (what this block *is*)

Four types. A block has at most one.

| Type | Meaning |
|---|---|
| `decision` | Something was decided, and why. A fact about the past. |
| `blocker` | Something is stuck, or is at risk of getting stuck. |
| `insight` | Something worth remembering, whether learned or generated. |
| `question` | Something open that has no answer yet. |

### Axis 2 — Task state (what must *happen*)

Three states, linear. Applies to actionable items; a block may be a task
regardless of its type.

`todo` → `waiting` → `done`

`waiting` **requires a person**. "Waiting" with no one to wait on is not a
state, it is a stalled task pretending otherwise. This is the axis's
opinionated constraint.

### Axis 3 — Person

Not a tag: an entity that can be referenced from any block, of any type, in any
state. People accumulate a view of everything referencing them.

### Priority (attributes, not taxonomy)

`important` and `urgent` are boolean attributes of a task, not marks. They
answer "what do I do now", not "what is this". Keeping them out of Axis 1 is
what stops the vocabulary from re-inflating.

The single view of all captured tasks — the practice that survived two tool
migrations — remains possible; it becomes a property of the view, not of the
vocabulary.

## What was cut, and why

Traceability matters more than the list itself: these cuts are the opinion.

| Cut | Absorbed by | Reason |
|---|---|---|
| `risco` | `blocker` | A blocker is a realised risk. Same object, two states — not two objects. Unrealised risks are rarely reopened and become noise. |
| `aprendi` | `insight` | The distinction was origin (external vs. internal). Hesitation at marking time violates P-B: marking must be instant. |
| `pessoa` as a tag | Axis 3 | An entity, not a classification. |
| `importante` / `urgente` as tags | attributes | Prioritisation, not classification. |

Nine concepts became seven, across three axes that never compete for the same
decision.

## What was added

`question` is the only concept **added** rather than derived from two years of
use. Justification: an open question is the one thing the maintainer's three
template generations never had a home for (`risco` was an attempt), and it is
the natural future bridge to pillar 2 without automatic promotion of notes.

**It is also the weakest item here, so it carries a kill criterion:**

> If `question` is not used at least once a week during the first two months of
> real use, it is removed from the product — not documented as underused.

The same standard applies to any type: a mark nobody uses is a wrong default.

## Composition rules

- A block has **at most one** type. Forcing a choice keeps marking fast; a
  block that seems to need two is usually two blocks.
- Any block may be a task, in any state.
- Any block may reference any number of people.
- `waiting` requires at least one person.
- Untyped, untasked blocks are the **default and the majority**. Most of the
  day's stream is just writing. Per P-C, views show only what was marked —
  unmarked content is never surfaced automatically.

## Open for F3.3 (prototype)

Deliberately not decided here, because they are interface questions:

- How a mark is applied without leaving the keyboard or breaking the sentence.
- Whether types are visible in the stream or only in views.
- How `waiting` prompts for a person without becoming a form.
- What the check-out audit looks like, given it is the MVP's primary instrument
  (`success-metrics.md`).