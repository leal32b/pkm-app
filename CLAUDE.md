# Repository contract

Rules for any AI agent or human working in this repository. Read this file and
`docs/PROGRESS.md` before doing anything.

## Project

`pkm-app` — an opinionated, offline-first desktop PKM application.
Solo maintainer, 5-10h/week. Optimize for low rework, not for speed.

## Current state

**Documentation phase.** No application code exists yet. Do not scaffold the
app, install dependencies, or write source files until `docs/PROGRESS.md`
states that phase F5 has started.

## Language

- Conversation with the maintainer: **pt-BR**.
- Everything committed to this repository — code, identifiers, comments, file
  names, commit messages, documentation: **English**. No exceptions.

## Stack

- Core: **Rust** via **Tauri**. The maintainer has zero Rust experience — keep
  the core thin, prefer clarity over cleverness, and explain unfamiliar idioms.
- Frontend: **SolidJS** + TypeScript.
- Before asserting anything about Tauri APIs, plugins or configuration, **consult
  the official docs for the version pinned in this repo**. The API changed
  significantly across major versions; do not answer from memory.

## Conventions

- **Commits:** [Conventional Commits](https://www.conventionalcommits.org),
  signed off (`git commit -s`) per DCO. Example:
  `docs: add ADR 0003 (core/UI boundary)`
- **Branching:** trunk-based. Short-lived branches merged into `main` quickly.
  `main` must always be in a working state.
- **Docs:** [Diátaxis](https://diataxis.fr) — tutorials, how-to guides,
  reference, explanation. Every document starts with a front-matter header:
  `status`, `date`, `version`, and links to the artifacts it derives from.
- **Decisions:** recorded as ADRs in `docs/adr/`, sequentially numbered.
  ADRs are immutable; a changed decision gets a new ADR that supersedes the old.

## Never do

- Never write application code before the corresponding ADR exists.
- Never add a runtime dependency without recording why. Every dependency is a
  liability for a solo maintainer.
- Never introduce a configuration option to avoid making a product decision.
  This project is opinionated by design — defaults are the product.
- Never add a third-party plugin API. Scope is deliberately closed (ADR 0002).
- Never widen Tauri capabilities/permissions beyond what the current feature
  needs. Permissions are part of the threat model, not configuration.
- Never commit secrets, signing keys or updater private keys.
- Never invent market data, user research or benchmarks. Mark inferences as
  `[ASSUMPTION]`.

## Commands

None yet. This section is filled in when the project is scaffolded (F5).