# pkm-app

> Working title. Naming is a product decision, deferred to F2/F3.

An opinionated, offline-first personal knowledge management app for the desktop.

## Status

**Pre-alpha — not usable yet.** There is no code in this repository, only
product and architecture documentation. Development starts once the discovery
and design phases produce a defined MVP scope.

Follow the project state in [`docs/PROGRESS.md`](docs/PROGRESS.md).

## What this is meant to be

Existing PKM tools trade configurability for cognitive overhead: the user is
asked to make dozens of decisions before writing a single note. This project
takes the opposite bet — **strong defaults over configuration**, a closed and
deliberate feature scope, and no third-party plugin ecosystem.

Non-negotiable constraints:

- **Offline-first.** The app is fully functional with no network connection.
- **Light and fast.** Startup and interaction latency are treated as features.
- **Elegant.** The interface is designed, not assembled.

Target platforms: macOS (primary), Windows, Linux.
Distribution: GitHub Releases and Homebrew. No app stores.

## Tech stack

[Tauri](https://tauri.app) (Rust core) with a [SolidJS](https://www.solidjs.com)
frontend. Rationale and revisit triggers are recorded in `docs/adr/`.

## Documentation

- [`docs/PROGRESS.md`](docs/PROGRESS.md) — current phase, decisions, open questions
- [`docs/adr/`](docs/adr/) — architecture and product decision records
- [`CLAUDE.md`](CLAUDE.md) — repository contract and conventions

## Contributing

The project is not open for contributions yet; the scope is still being defined.
Contributions will be accepted under the
[Developer Certificate of Origin](https://developercertificate.org/) — every
commit must carry a `Signed-off-by` line (`git commit -s`). No CLA is required.

## License

[AGPL-3.0-or-later](LICENSE). See `docs/adr/0002-license-agpl-3-0.md` for the
reasoning behind this choice.