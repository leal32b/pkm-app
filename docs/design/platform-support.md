---
status: accepted
date: 2026-08-22
version: 1.0
phase: F3
source: docs/product/vision.md
constrains: F4 (architecture), F5 (CI matrix)
verified against: Tauri v2 official docs, 2026-08-22
---

# Platform support

## Support tiers

| Tier | Platforms | Commitment |
|---|---|---|
| **Primary** | macOS (Apple Silicon) | Developed on, launched and used daily, blocks release |
| **Best effort** | Windows 11, Ubuntu LTS | Built in CI every commit; **never launched by the maintainer**. Bugs are accepted and triaged but do not block release. |
| **Unsupported** | everything else | Not built, not promised |

**Only macOS is verified.** The maintainer has no access to a Windows or Linux
machine, so the other two are compiled but never run. CI proves the code
compiles; it says nothing about whether the webview renders correctly — and
webview divergence is precisely the risk this document exists to name.

Calling them "supported" would be a promise that cannot be kept. The gap is
recorded here so it is a known limitation rather than a discovered one.

### What this obliges

- **README states it plainly** from the first release: verified on macOS,
  best-effort elsewhere, help wanted.
- **Linux and Windows bugs are not release blockers.** A solo maintainer cannot
  debug a rendering issue on a machine he does not have.
- **This is the strongest argument for a design that stays inside the common
  subset of all three engines** — see below. Restraint is not aesthetic here,
  it is the only available substitute for testing.

### How the gap could close

Cheapest first, none of them required for the MVP:

1. **A first Linux or Windows user who reports back.** Free, and the most likely
   path. The README's "help wanted" exists for this.
2. **A Windows VM or a cheap used machine.** Modest cost, real verification.
3. **Screenshot tests in CI.** Catches gross rendering breakage without a
   machine, but is real engineering effort and belongs to F7 at the earliest.

Promoting a platform to Primary requires the maintainer to actually launch and
use the app there. Nothing less counts.

## Why the WebView matters more here than in a web app

Tauri renders through the **system** webview, not a bundled one: WKWebView on
macOS, WebView2 on Windows, WebKitGTK on Linux. Three engines, three sets of
rendering bugs, and no bundled runtime to normalise them.

**macOS is the constraint, not the safe case.** The system WebKit updates only
with the OS, so the oldest supported macOS defines the CSS and JS baseline for
the whole product. Testing only on the maintainer's up-to-date machine will
hide breakage on older Macs.

**Linux is the loudest.** WebKitGTK versions vary widely across distributions,
and Tauri v2 requires the 4.1 series rather than 4.0. This is the documented
source of "only happens on Linux" bugs.

**Windows is the mildest.** WebView2 is Chromium-based and evergreen; it ships
with Windows 11 and recent Windows 10, and Tauri's installer can ensure it is
present.

### Consequence for design
The prototype's design must survive the **oldest** engine in the supported set.
Verify anything non-trivial (subgrid, container queries, `:has()`, newer text
features) against the macOS WebKit baseline before adopting it — see the version
tables in Tauri's webview-versions reference.

**Rule:** if a visual effect needs a feature that is not available across all
three engines, it does not ship. The design is quiet and typographic, which
makes this cheap to honour — a wall of gradients would not.

## Testing obligation

**The walking skeleton must be launched and used on macOS before F5 proceeds.**
On Windows and Linux, the obligation is only that CI produces an installable
artefact — nobody will open it. This is a known, accepted blind spot, not an
oversight.

This is why the CI matrix has to exist from the first skeleton (F4/F5): macOS
builds cannot be produced off a macOS machine, and deferring the matrix
accumulates debt that gets paid at the worst moment.

## OS conventions the product will follow

Deliberately shallow. A quiet, typographic app has few surfaces where native
conventions bite.

| Concern | Decision |
|---|---|
| Window chrome | Native title bar on each OS. No custom chrome — it is the most common source of platform-specific bugs and buys nothing here. |
| Primary modifier | `Cmd` on macOS, `Ctrl` on Windows and Linux. Shortcuts are defined once by role and mapped per platform. |
| Menu bar | macOS: real system menu bar. Windows/Linux: minimal or none — the app has almost no commands that are not keyboard-driven. |
| Fonts | System UI font on each platform. No bundled font in the MVP: bundling adds licence review and megabytes, and the design is weight-and-rhythm driven rather than face-driven. |
| Light / dark | Follows the OS setting. **Not a preference in-app** — an in-app toggle would be a settings screen (refusal 1). |
| Data location | Per-OS application data directory, resolved by Tauri. Never a user-chosen folder (refusal 1, and there is no vault picker). |

## Deferred to F4

- Whether a bundled font is worth the cost after the design settles.
- Notarisation and signing per OS: cost, lead time, and the Apple Developer
  account that is still not acquired.
- Whether the AppImage's larger size (it embeds the WebKitGTK runtime) is worth
  the compatibility it buys, versus `.deb`/`.rpm` that rely on the system's.