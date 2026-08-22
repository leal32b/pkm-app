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

`important` and `urgent` are boolean attributes of a task. Both exist; they are
not merged. They render as a **text suffix** at the end of the block, never
inside the sentence:

`☐ Write the runbook for the cutover · important`

The suffix doubles as the edit affordance — a priority that cannot be changed
without opening a menu is a priority nobody maintains.

**Suffixes work only while they are rare.** One suffix is a tail; four are a
train. That is the reason the budget below is closed.

## Symbol budget

| Channel | Contents | Rule |
|---|---|---|
| Gutter | four note types | one per block, exclusive |
| Glyphs | `☐` todo · `◷` waiting · `☑` done | **three, closed** — exclusive states only |
| Suffix | `important`, `urgent` | optional attributes, text not symbols |
| Inline | `@[[person]]`, `[[note]]` | closed (see Reference syntax) |

**Glyphs are for exclusive states. Text is for optional attributes.** Adding
optional, combinable symbols turns recognition into decoding — the criticism
recorded against Tana in `market-pain-research.md`, and incompatible with a
product that promises value on day one.

## Deliberately excluded: due dates and scheduling

Neither exists in the MVP.

**Due dates** were considered because `waiting on @someone` with no sense of
time is hard to act on. That need is met by derivation instead of input: every
block already records when it was written, so elapsed time is computed, not
typed — `◷ @Marina — rollback plan    waiting 3 days`. No new field, no new
concept, no new decision for the user (P-C).

**Scheduling** is telling a future self what to do — the aspirational capture
refusal 2 forbids, and something the maintainer cut from his own template
(archaeology, C3). A journal with scheduling is a task manager, and that is a
crowded quadrant this product did not choose.

Both fall under the revision trigger above: if real use shows the need, it
becomes an ADR, not a quiet addition.

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

## Hierarchy

Blocks nest **exactly one level deep**. A block may have children; a child may
not. A parent is usually context (a meeting, a topic), and its children are what
came out of it.

14:00     1:1 with @Rafael
            ☐ TODO wants more scope on [[Platform team]] roadmap work
10:20     decision · going with expand-and-contract
            ☐ TODO write the runbook for the cutover · important

A child may carry a type, a task state and people. It does **not** carry its own
timestamp: the parent is the moment, and the children belong to it. This keeps
the time column readable as the shape of the day rather than a stamp on every
line.

Derived durations on a child (`waiting 3 days`) are computed from the **parent's**
timestamp, which is also the more accurate answer — the wait began at the
conversation, not at the moment the line was typed.

**Why one level rather than none or many.** A flat stream forces context to be
repeated in every line, which does not match real use. Unlimited nesting — the
Logseq and Roam model — reintroduces "where does this go?" at every level,
which is the decision this product exists to remove. One level covers the real
case (context → items) and makes depth a binary rather than a judgement: a
block is a child or it is not. There is never a decision about how deep.

**Accepted cost:** users coming from an outliner will hit the limit. This is the
same class of constraint as `waiting` requiring a person — it removes a question
rather than an ability.

## Visual channels

The three axes are independent, so they need independent channels. Collapsing
them into one lane makes a block unable to be, say, both a `blocker` and a task
— which the F3.3 prototype exposed.

| Axis | Channel |
|---|---|
| 1 — Note type | left gutter, outside the text column |
| 2 — Task state | icon plus word at the start of the text |
| 3 — Person | inline in the sentence |

A block therefore shows its type and its task state at once, without competing
for the same slot.

Timestamps sit in the gutter between the type mark and the text (top-level
blocks only — see Hierarchy). Priority renders as a text suffix after the
sentence.

### Task state rendering

| State | Icon (Tabler) | Word |
|---|---|---|
| `todo` | `ti-square-rounded` | `todo` |
| `waiting` | `ti-square-rounded` | `waiting`, followed by the person |
| `done` | `ti-square-rounded-check` | `done` |

**The icon says it is a task and whether it is finished; the word says the
state.** `todo` and `waiting` share the empty box because both are open. A third
similar icon would force decoding instead of recognition (symbol rule).

Icons render at 18-20px, larger than the surrounding body text, so the task
column scans at a glance. Words are lowercase — the product is quiet.

09:40 blocker ☐ todo Staging deploys failing on the migration
09:44 ☐ waiting @Marina — rollback plan before we retry
11:05 ☐ todo Write the runbook · important
16:40 ☑ done Reviewed the RFC


### No derived durations in the journal

A `waiting` block shows no elapsed time. In the day it was captured, the elapsed
time is always zero — the wait starts there. Duration is meaningful only in an
aggregate task view across days, which is out of scope for the MVP and belongs
to F7.

### Person placement
When a block is `waiting`, the person follows the word directly:
`☐ waiting @Marina — rollback plan`. Elsewhere, a person may appear anywhere in
the sentence.

### Enforcing the `waiting` constraint
Choosing `waiting` opens the person picker immediately. Dismissing the picker
leaves the block as `todo`. **There is no error message and no invalid state** —
the constraint is satisfied by the flow, not by validation.

### Timestamps
Every top-level block records the time of its **first keystroke**, not of its
creation. An empty block shows no time. The time is **always displayed**,
quietly, in the gutter.

It is **editable** — a block written at 14:00 about a 09:00 conversation should
carry 09:00. It is **not removable**: a missing time breaks the column, and
per-block visibility would be a configuration decision.

Whether to display the time is not a user setting. Offering hidden / visible /
on-hover would be a settings screen in disguise (refusal 1). The app decides:
always visible.

## Open for F3.3 (prototype)

Interface questions, deliberately not decided here:

- How a type is applied without leaving the keyboard or breaking the sentence
  (command palette, `#` with a closed list of four, or something else — the
  vocabulary is locked either way).
- Whether types are visible in the stream or only in views.
- Whether an unknown `@name` silently creates a person, offers to, or does nothing.
- What the check-out audit looks like, given it is the MVP's primary instrument
  (`success-metrics.md`).