# Changelog

## v2.0.7 (2026-06-15)

**Installer + fewer antivirus false positives.**

### Changed
- NullSync now ships as a small installer instead of a single loose .exe. It installs per-user (no admin needed) and adds a Start menu shortcut. This packaging trips far fewer antivirus false positives than the previous single-file build.
- The anonymous install count is now sent only after the app has been open for a while, rather than right at launch. Short sessions never send anything, and it avoids the "connects to a server the moment it starts" pattern that antivirus tools flag. It is still tied to the "check for updates on startup" toggle and stays anonymous (hashed machine identifier, app name, and version only).

### Added
- An [ANTIVIRUS](ANTIVIRUS.md) page explaining why compiled apps like this sometimes get flagged, how to confirm it is a false positive on VirusTotal, and how to allow it.

## v2.0.6 (2026-06-15)

**Update notifications + build improvements.**

### Added
- Startup update check. NullSync now checks for a newer release when it launches and shows a clickable banner at the top of the window when one is available. Respects the "check for updates on startup" toggle in Settings. Before this, checking for updates was a manual button in Settings only.

### Changed
- Build and packaging improvements under the hood. No change to how the app works day to day.

## v2.0.5 (2026-05-16)

**Themed alert dialogs.** Every alert and confirmation popup now uses NullSync's gold-on-black look instead of the stark default Windows message box, so they're easier to read and consistent with the rest of the app.

## v2.0.4 (2026-05-16)

**Splash polish.** Cleaned up the startup splash so it reads as a brand reveal rather than a generic loading screen, and removed a brief flash of the UI before the splash appeared.

## v2.0.3 (2026-05-16)

**Polish and edge-case fixes.**
- Fixed the app icon and mascot images not loading in the released build.
- Fixed a case where activating a license in one tab wasn't reflected when picking a premium theme in another.
- The Terms of Service prompt now shows the NullSync icon.

## v2.0.2 (2026-05-16)

- The Help button now opens a proper themed help dialog.
- Compare results let you expand each mismatched mod to see a file-by-file breakdown, sorted by how much each difference matters.
- Much smaller download (around 73 MB, down from 275 MB) by trimming unused components.

## v2.0.1 (2026-05-16)

- Terms of Service prompt restored on launch, with a scrollable accept and decline dialog.
- Added a startup splash that holds briefly, then fades into the app.

## v2.0.0 (2026-05-16)

**Full UI rewrite.** NullSync moved to a new interface with the polished gold-on-black look of the wider Nullcore family.

### Highlights
- Borderless window with a custom title bar (drag, double-click to maximize, gold-glow window buttons).
- Windows 11 acrylic glass backdrop with subtle animated background detail.
- Stylized NULLSYNC wordmark and BETA badge.
- Every control themed end to end: buttons, inputs, dropdowns, scrollbars, progress bars, switches.
- All tabs carried over: Fingerprint, Compare, Diagnose, Settings, License, About.
- Your settings, saved theme, Stellaris folder, and agreements carry over from earlier versions, and fingerprints made in older versions still compare correctly.

## v1.4.2 (2026-05-16)

- Theme polish: removed the last blue tints on tabs and buttons, added the BETA badge, and themed the remaining stragglers (scrollbars, dropdowns, switches, sliders, inputs).

## v1.4.1 (2026-05-16)

- Glass effect now reliably applies on Windows 11.
- Fixed the animated background detail not showing.
- Warmer, richer gold tone.

## v1.4.0 (2026-05-16)

**Nullcore theme + anonymous install count.**
- New default "Nullcore" gold-on-black theme. Existing themes (Sakura, Cobalt, Midnight) still available.
- Animated gold background detail and a stylized NULLSYNC wordmark.
- Windows 11 acrylic glass backdrop on by default for the Nullcore theme.
- Added an anonymous, once-a-day "install exists" ping so the project can count unique installs rather than raw download totals. It sends only a hashed machine identifier (hashed on your device), the app name, and the version. No personal data. Turned off by the same "check for updates on startup" toggle, and disclosed in the updated Terms of Service.

## v1.3.7 (2026-05-13)
- Added a "looking for testers" invite to the splash, the About tab, and the README.

## v1.3.6 (2026-05-13)

**Plain English over jargon.**
- Compare results now name which player needs to update a mod, with plain action items and step-by-step reinstall instructions.
- Section headers and verdicts reworded from checksum-speak to plain outcomes (whether you'll actually connect).

## v1.3.5 (2026-05-13)

**Stability and diagnostics.**
- Added a sanitized activity log and a crash log under your settings folder (no usernames, share codes, or license keys), plus About > Bug Reports buttons to open the log folder and copy diagnostic info.
- A single broken mod no longer aborts a whole scan; it's skipped with a reason instead.
- Faster scans on large mod lists.

## v1.3.4 (2026-05-13)
- Added an "early version" notice to the splash and About tab inviting bug reports.

## v1.3.3 (2026-05-13)
- Renamed "predicted checksum" to "sync checksum" everywhere to better reflect what it does: a deterministic value from your setup that, when it matches a friend's, means your setups are compatible.

## v1.3.2 (2026-05-13)
- Added an in-development teaser to the splash for an upcoming Stellaris fleet mod.

## v1.3.1 (2026-05-13)

First public release.

**Core features**
- Fingerprints your active Stellaris mod setup: load order, file integrity, descriptor info, sync checksum.
- Shareable codes for comparing setups with a friend.
- Side-by-side compare with mismatch attribution, version detection, file-level differences, and missing-dependency surfacing.
- Diagnose tab: broken Workshop subscriptions, mods with critical errors, and missing dependencies.

**App experience**
- About tab with project info, community links, and credits.
- License tab for upcoming premium features.
- Sakura theme (free), plus Cobalt and Midnight premium themes.
- Windows 11 Acrylic glass effect as a premium visual option.
- Terms of Service prompt on first launch.
- Brief welcome panel for free users with community links and my Stellaris Workshop mods.
- On-startup update notifier with a dismissible banner. Can be turned off in Settings.
