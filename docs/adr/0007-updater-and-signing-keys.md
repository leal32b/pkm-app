---
status: accepted
date: 2026-08-22
version: 1.0
related: docs/adr/0004-tauri-and-solidjs.md, docs/product/mvp-spec.md
verified against: Tauri v2 updater docs, 2026-08-22
---

# 7. Updater strategy and signing keys

## Context

The auto-updater is out of scope for v0.1 (`mvp-spec.md`). This ADR exists
anyway, because one part of it **cannot be deferred**.

Tauri's updater requires a signature to verify an update comes from a trusted
source, and this cannot be disabled. The private key signs the installers. It
must never be shared, and **losing it makes it impossible to publish updates to
anyone who has already installed the app**. There is no recovery: the only path
would be asking every user to manually reinstall from a new key.

Generating the key costs five minutes now. Discovering later that it was never
generated, or was lost, permanently strands the installed base.

## Decision

### 1. Generate the key pair now, before the first release
```
npm run tauri signer generate -- -w ~/.tauri/pkm-app.key
```

Produces a private key (`pkm-app.key`) and a public key (`.key.pub`), and
prompts for a password protecting the private key.

**Both the key and its password are irreplaceable.** Store them in a password
manager — not only on the development machine, whose loss would take the
project's future with it.

The public key is safe to publish and goes into `tauri.conf.json` when the
updater is enabled.

### 2. Never commit the private key

`.gitignore` covers `*.key` and `.env` from the first commit of the scaffold.
When CI signs builds (F6), the key and password become repository secrets, set
as `TAURI_SIGNING_PRIVATE_KEY` and `TAURI_SIGNING_PRIVATE_KEY_PASSWORD`.

Note that Tauri reads these from the environment; `.env` files are not picked up
by the build.

### 3. The manifest is a static file in GitHub Releases

When the updater ships, the endpoint is a `latest.json` published as a release
asset. No server, no third-party service, nothing to run or pay for — consistent
with a solo maintainer and with distribution already happening through GitHub
Releases.

Deferred until then: whether the app checks automatically or only on request.
**Constraint recorded now:** an update check is a network request, so it must be
compatible with the offline-first principle — the app must be fully usable with
no network, and a failed check must be silent.

### 4. Do not enable the updater in v0.1

The updater is not merely a feature; it is a distribution mechanism that can
break every installed copy. Enabling it before the app is signed and notarised
(`platform-support.md`) means shipping an unsigned auto-update pipeline, which
is worse than having none.

**Order is fixed:** signing and notarisation first, updater second.

## Consequences

- One irreversible task moves from F6 into this week, where it is cheap.
- The scaffold ignores key files from its first commit — a private key committed
  once is compromised, even if removed later.
- v0.1 users update by downloading a new release manually. Acceptable for a
  handful of deliberate early users; not acceptable at any scale.

## Revision triggers

1. **The private key is lost or compromised.** Stop everything. A new key means
   the existing installed base can never auto-update again and must be told to
   reinstall.
2. The static manifest in GitHub Releases proves insufficient — for example if
   staged rollouts become necessary.