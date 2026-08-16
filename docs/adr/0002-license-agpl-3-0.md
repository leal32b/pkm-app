---
status: accepted
date: 2026-08-16
version: 1.0
related: docs/adr/0001-record-architecture-decisions.md
source: copilot session 2026-08-16 (F0 licensing discussion)
---

# 2. License the project under AGPL-3.0 with DCO

## Context
The project is an open source, offline-first desktop PKM application, built by a
single maintainer. Two constraints shape the licensing choice:

1. The likely monetization path is a **paid optional sync/backup service**, delivered
   as a separate network service. Premium features gated inside the distributed binary
   are explicitly not the plan (and would be weak anyway: a distributed binary is
   inspectable, so local-only gating is trivially bypassed).
2. The product is intentionally **closed in scope**: no third-party plugin ecosystem.
   Extensibility is therefore not an argument for a permissive license.

Options considered: Apache-2.0, GPL-3.0, AGPL-3.0.

## Decision
License the project under **AGPL-3.0-or-later**.

Accept contributions under the **Developer Certificate of Origin (DCO)**, requiring a
`Signed-off-by` line on every commit. **No CLA** is required.

## Consequences
- A third party cannot take this codebase, close it, and offer it as a hosted service.
- A future paid sync service, implemented as a separate codebase with a network API,
  is unaffected by the AGPL obligations of this repository.
- Because there is no CLA, the copyright is distributed across contributors. The project
  **cannot be relicensed or dual-licensed** later without unanimous consent. This is an
  accepted, deliberate trade-off: it closes the "open core inside the binary" path for good.
- Contributors are not asked to assign rights, which lowers the barrier to contribute.
- All bundled dependencies must be license-compatible with AGPL-3.0. Rust crates and
  npm packages are predominantly MIT/Apache-2.0, which is compatible. This must be
  verified in CI before the first public release (F6).
- `LICENSE` at the repository root, SPDX identifier `AGPL-3.0-or-later`.

## Revisit triggers
- Monetization shifts away from a separate network service.
- A decision to open a third-party plugin ecosystem.