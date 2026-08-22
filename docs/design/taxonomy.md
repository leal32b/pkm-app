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
shipping two badly. This is a product decision, distinct from the repository's
English-only rule in `CLAUDE.md`.

## Three axes, not one list

The maintainer's previous system had nine concepts because one mechanism
(inline tags) carried three different kinds of meaning. Separating them shrinks
each axis to something a person can hold in their head.

### Axis 1 — Note type (what this block *is*)

Four types. A block has at most one.

| Type | Meaning |
|---|---|
| `decision` | Something was decided, and why. A fact about the past. |
| `blocker` | Something is stuck, or at risk of getting stuck. |
| `insight` | Something worth remembering, whether learned or generated. |
| `question` | Something open that has no answer yet. |

### Axis 2 — Task state (what must *happen*)

Three states, linear. A block may be a task regardless of its type.

`todo` → `waiting` → `done`

`waiting` **requires a person**. "Waiting" with nobody to wait on is not a
state, it is a stalled task pretending otherwise. This is the axis's
opinionated constraint, and it is the one most likely to attract requests to
relax it. The answer is no (refusal 3).

### Axis 3 — Person

Not a type: an entity referenced from any block, in any state. A person is a
note with a special role, and accumulates a view of everything referencing them.

### Priority — attributes, not taxonomy

`important` and `urgent` are boolean attributes of a task, not marks. They
answer "what do I do now", not "what is this". Keeping them out of Axis 1 is
what stops the vocabulary from re-inflating.

The single view of all captured tasks — the practice that survived two tool
migrations — remains possible; it becomes a property of the view, not of the
vocabulary.

## What was cut, and why

Traceability matters more than the list: these cuts *are* the opinion.

| Cut | Absorbed by | Reason |
|---|---|---|
| `risco` | `blocker` | A blocker is a realised risk. Same object, two states — not two objects. Unrealised risks are rarely reopened and become noise. |
| `aprendi` | `insight` | The distinction was origin (external vs. internal). Hesitation at marking time violates P-B: marking must be instant. |
| `pessoa` as a tag | Axis 3 | An entity, not a classification. |
| `importante` / `urgente` as tags | attributes | Prioritisation, not classification. |
| **free-form tags (`#`)** | `[[ ]]` notes | See below. |

Nine concepts became seven, across three axes that never compete for the same
decision.

### Why there are no free-form tags

A tag is a label: it filters, and nothing else. A note is a place: it filters
*and* holds content, context and backlinks. **A note does everything a tag does
and more**, so a product that ships both forces a decision mid-sentence — "is
this a tag or a note?" — that nobody answers consistently. The same subject ends
up marked both ways and half of it is lost at retrieval time.

The evidence is in the maintainer's own history: `#importante`, `#urgente`,
`#rotina`, `#recorrente`, `#nota_diária`, `#gupy` — six vocabularies invented
over two years, and the template that finally worked is the one that cut nearly
all of them. Free-form tags never hurt to create individually, which is exactly
how a system accumulates fifteen of them and needs "fixing" again.

Everything previously tagged has a home: types are marks, priority is an
attribute, people are `@[[ ]]`, and every other subject — project, product,
team, book, concept — is a note.

## What was added

`question` is the only concept **added** rather than derived from real use.
Justification: an open question is the one thing the three template generations
never had a home for (`risco` was an attempt), and it is the natural future
bridge to pillar 2 without automatic promotion of notes.

It is the weakest item here, so it carries a kill criterion:

> If `question` is not used at least once a week during the first two months of
> real use, it is removed from the product — not documented as underused.

The same standard applies to any type: **a mark nobody uses is a wrong default.**

## Reference syntax

Two forms, and the list is closed for the MVP.

| Form | Refers to | Rendered as |
|---|---|---|
| `@[[Ana Silva]]` | a **person** (Axis 3) | `@Ana Silva` |
| `[[Postgres migration]]` | a **note** | as written |

**Why people get distinct syntax.** People are the only entity the product
models explicitly, and `waiting` requires one. Distinct syntax makes the
requirement expressible without a form, and reads as prose mid-sentence:
*waiting on @Ana Silva for the migration plan*.

**How it is typed.** The user types `@`; a picker offers existing people and the
option to create one; on Enter the app writes the full `@[[ ]]` form. The stored
text is explicit and greppable; the displayed text is short.

**Collisions are structurally impossible.** Because a reference only exists
after the picker, pasted content is always literal: `user@example.com`,
`@scope/pkg`, `@Component`, `@media`, pasted Slack mentions. The target user
pastes code into their journal, so this is not a theoretical concern. No
heuristics, no escaping rules.

### Syntax budget
The list above is **closed**. A third form requires an ADR, not an
implementation decision. Sigil proliferation is configuration inflation
arriving through syntax.

## Revision trigger

The vocabulary is locked for v0.1, **not forever**. Locking first is the
reversible choice: adding free-form tags later breaks nothing, while removing
them later breaks every installed user's system — the retroactive-change failure
mode documented in `market-pain-research.md` (N1).

> If real use produces recurring requests for a fifth concept, it becomes an
> ADR. Either the concept ships as a new default (a new opinion), or the
> vocabulary opens (the opinion is abandoned). The decision is made explicitly,
> never by accident.

## Composition rules

- A block has **at most one** type. A block that seems to need two is usually
  two blocks.
- Any block may be a task, in any state.
- Any block may reference any number of people and notes.
- `waiting` requires at least one person.
- Untyped, untasked blocks are the **default and the majority**. Most of the
  day's stream is just writing. Per P-C, views show only what was marked;
  unmarked content is never surfaced automatically.

## Open for F3.3 (prototype)

Interface questions, deliberately not decided here:

- How a type is applied without leaving the keyboard or breaking the sentence
  (command palette, `#` with a closed list of four, or something else — the
  vocabulary is locked either way).
- Whether types are visible in the stream or only in views.
- Whether an unknown `@name` silently creates a person, offers to, or does nothing.
- What the check-out audit looks like, given it is the MVP's primary instrument
  (`success-metrics.md`).