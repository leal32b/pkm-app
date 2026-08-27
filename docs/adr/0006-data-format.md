---
status: accepted
date: 2026-08-22
version: 1.0
related: docs/adr/0005-core-ui-boundary.md
constrains: F5, and every future version of the product
---

# 6. Data format — one Markdown file per day

## Context

This is the decision a solo-maintainer project cannot afford to get wrong.
Logseq began a database rewrite in late 2022; by April 2025 it had not shipped,
with roughly a year between releases, and the outcome was splitting the product
in two — with funding and a team. Migrating someone's journal is the most
dangerous operation this application will ever perform.

## Decision

### Files are the source of truth. Always.

One **Markdown file per day**, named `YYYY-MM-DD.md`, in the OS application data
directory.

**There is no database in v0.1.** When cross-day features arrive (backlinks, a
task index, search), an index may be added — but only ever as a **derived,
disposable cache** that can be deleted and rebuilt from the files. Two sources
of truth turn a local app into a distributed-systems problem, which is the
failure mode above.

### Format

```markdown
---
v: 1
date: 2026-08-20
focus: [b7k2, m4x9, p1c8]
intention: Protect two hours of deep work
---

- 09:40 {blocker} Staging deploys failing on the [[Postgres migration]]
  - schema diff tool times out on the users table
  - {todo|b7k2} @[[Marina]] — rollback plan before we retry
- 10:20 {decision} Going with expand-and-contract, not a maintenance window
  - {todo|m4x9} write the runbook for the cutover
- 14:00 1:1 with @[[Rafael]]
  - {question} do we need the schema diff at all?
- 16:40 {done|p1c8} Reviewed the RFC
```

- **Front matter** carries only what belongs to the day as a whole: format
  version, date, focus references, intention.
- **Marks** use `{ }` at the **start of a block's content only**. Type and task
  state share one mark: `{blocker}`, `{todo}`, `{todo|id}`, `{blocker todo|id}`.
- **Timestamps** on top-level blocks only, as the design requires.
- **Ids** exist only on tasks, and only so focus can reference them: 4-character,
  stable, never reused.

### Why the format survives its own stress tests

**Test 1 — pasted code containing `{` and `[[`.** Broke the first draft. Fixed
by two rules: a mark is only recognised at the **start of block content**, and
**fenced code blocks are never parsed**. `{"key": "value"}` mid-sentence is
literal text. This matters because the target user pastes stack traces into the
journal daily.

**Test 3 — focus and task state.** Broke the first draft, which stored state in
both the front matter and the task line — two sources of truth inside one file.
Fixed: **front matter stores ids only.** State is read from the task line, which
is the single place it lives. This is why focus references ids rather than text:
editing a task's wording must not break the link.

**Test 2 — a hand-deleted id.** Focus silently drops the reference. No error,
no repair attempt. Unknown data is preserved verbatim, never rewritten.

**Test 4 — git diffs.** One edited line produces one changed line. The core
never reformats, reorders or normalises a file it did not change.

**Test 5 — migration to v2 for note pages.** Nothing changes. `[[note]]` is
already stored as text in v0.1 (`mvp-spec.md`), so pages are built from data
already on disk. **No migration needed** — which is the whole point of shipping
the mark early.

**Test 6 — a corrupt or half-written file.** The core opens what it can and
**never rewrites a file it failed to fully parse**. A day that cannot be read is
shown read-only with a plain message. Silent repair is forbidden: a wrong repair
destroys the original, and there are no backups in v0.1.

### External editing

The format is designed for it, and the app's behaviour is deliberately minimal
in v0.1: **on window focus, re-read the file; if it differs from what is on
screen, the disk wins and the view updates.** No merge, no conflict dialog.

This covers the real case — edit in VS Code, return to the app — in roughly 30
lines rather than 300. It does not cover editing in both places simultaneously,
which is acceptable for a single user on one machine.

**Consequence:** the folder can be put in git or a sync folder, and diffs are
readable. Sync itself remains out of scope.

### Versioning and migration

`v: 1` in the front matter. Rules, permanent:

1. **Additive changes do not bump the version.** A new optional field an older
   build ignores is not a migration.
2. **A bump requires a written migration and a backup of the whole data
   directory before it runs.**
3. **Never migrate in place.** Write the new version alongside, verify, then
   replace.
4. **A file whose version is newer than the running build opens read-only.**
   Better to refuse than to corrupt.

## Consequences

**Accepted**
- Reading many days means reading many files. Fine for v0.1 (a day is opened at
  a time); the reason an index is allowed later.
- `{ }` marks are not standard Markdown, so another editor renders them as
  literal text. Acceptable: the file stays readable and nothing is lost.
- Front matter is YAML, which brings a parsing dependency into the core.

**Rejected**
- **SQLite as the source of truth.** Faster queries, worse everything else:
  opaque to `grep`, hostile to git and to any sync folder, and it makes the app
  the only thing that can read the user's notes. A solo-maintainer project
  holding personal notes must survive its maintainer.
- **JSON.** Robust and unreadable by hand, which defeats external editing.
- **One file per month.** Fewer files, but every edit rewrites a large file and
  git diffs get worse.

## Revision triggers

1. Opening a day becomes slow — which would mean days grew far beyond expectation.
2. Cross-day features need an index. **Add a derived cache; do not move the
   source of truth.**
3. Two files are ever observed to disagree about the same fact. That means a
   second source of truth crept in, and it must be removed.