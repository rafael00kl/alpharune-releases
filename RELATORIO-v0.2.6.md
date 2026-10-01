Maintained by **Fargrim**. This is the historical AlphaRune v0.2.6 report. The active project is [Rifteemo](https://github.com/rafael00kl/rifteemo-releases). Historical binary asset names are preserved.

# AlphaRune 0.2.6 distribution report

## Links

- Private source project: https://github.com/rafael00kl/rifteemo
- Public project/download instructions: https://github.com/rafael00kl/alpharune-releases
- Stable release: https://github.com/rafael00kl/alpharune-releases/releases/tag/v0.2.6
- Latest installer: https://github.com/rafael00kl/alpharune-releases/releases/latest/download/AlphaRune-Setup.exe
- Versioned installer: https://github.com/rafael00kl/alpharune-releases/releases/download/v0.2.6/AlphaRune-Setup.exe
- Versioned launcher: https://github.com/rafael00kl/alpharune-releases/releases/download/v0.2.6/AlphaRune.exe
- [Installation and updates](https://github.com/rafael00kl/rifteemo-releases#installation-and-updates)

The public release repository has its own documentation history; it does not contain or merge the private engine source history. Runtime frontend/Python files are shipped as required by the existing architecture. Actual source commit, validation input/binary hashes, platform and package checksum are recorded in release-manifest.json. VERSION is 0.2.6.

## Completed implementation

- Independent Setup provisions compatible Ubuntu 26.04 x64 in WSL when necessary and installs Python/CA/Boost runtime libraries. It verifies Edge availability, fetches the latest public stable manifest/package, checks SHA-256, stages a version and installs launcher/shortcuts.
- Existing development code and legacy installer are preserved. Existing developer Windows config is retained; release shell can live beside it in AlphaRuneRelease.
- Startup and manual update checks compare stable numeric SemVer, requiring validated manifests matching the tag. Install Update & Restart requires confirmation, no unsaved edit and no active match.
- A worker starts and verifies a new client before atomically activating its version. On startup failure it recovers the previous client. Previous version folders are retained. Developer checkouts cannot receive packaged updates.
- Decks, config and client cache are shared between versions; shipped defaults do not overwrite existing user files. Browser preferences use a persistent launcher profile.
- Ordinary game updates do not rebuild the installer. This first updater applies complete runtime packages; data-only delivery remains a future compatible-manifest feature.
- Fixed runtime entrypoint validation and JavaScript handler scoping discovered while testing installed packages. No game/card rule changes.

## Validation evidence

- 1066 C++ tests passed; one pre-existing disabled test remains disabled.
- 8 client tests, 11 card-health tests, 7 release integrity/version/extraction tests and 5 runtime activation/shared-data/recovery/resume tests passed.
- Card coverage gate and random smoke simulations passed. Existing card-pool implementation status is unchanged by this release.
- Real Windows AlphaRune-Setup.exe and installed AlphaRune.exe executed successfully in isolated directories/ports, against the validated local runtime package.
- Packaged Python client served HTTP status, cards, UI and a real C++ human-versus-human game page on isolated ports. The smoke match was stopped after verification.
- API-driven transition using real 0.2.5 and 0.2.6 engines passed. Only remote release discovery/download was injected for that prepublication test. New registry loaded, shared user deck survived, old runtime retained.
- Full validation reruns on committed source bind the distributed files to their source commit. Public download acceptance is performed after publication and recorded in the completion report.

## Scope and limits

This is the first stable distribution channel for development use, not certification of every card or every Windows setup scenario. Windows x64 + Ubuntu 26.04 x86_64 is the supported package platform. Setup may require administrator consent, Ubuntu initialization and a Windows reboot; rerun it afterward. Edge is required and is not silently installed.

Interactive installation on a clean Windows machine without WSL, UAC/reboot/resume acceptance and browser visual acceptance were not exercised in this environment. The computer-use runtime was unavailable; real executables and HTTP/engine behavior were verified directly. This limitation is disclosed rather than claimed as a completed clean-PC test.

No mass card additions, gameplay changes, upstream pushes, source-publicity change or overwriting of older releases. Merge/tag/publication is limited to the user-authorized first release. Ignored builds, caches, reports, local launcher config and credentials stay outside source control.
