---
status: accepted
date: 2026-08-16
version: 1.0
supersedes: none
---

# 1. Record architecture decisions

## Context
This is a solo project with long gaps between sessions (5-10h/week). Decisions made
under context that is later forgotten get silently reverted or re-litigated.

## Decision
We record every non-trivial decision as an ADR in `docs/adr/`, numbered sequentially,
using the format described by Michael Nygard. Scope is not limited to architecture:
product, process, licensing and design decisions are recorded here as well.

ADRs are immutable once accepted. A decision that changes gets a new ADR that
supersedes the old one; the old file stays in place with `status: superseded`.

## Consequences
- Session start requires reading `docs/PROGRESS.md`, which links the active ADRs.
- Small cost per decision (~15 min) in exchange for not re-deciding.
- The ADR log doubles as the project's rationale documentation for future contributors.