# Changelog

## v2.0.2 (2026-05-16)

**Three things landed:** Help dialog wired up, Compare per-mod drill-down ported, and the exe is now **73 MB** (down from 275 MB).

### Added
- **Help dialog** — the banner's Help button now opens a real themed Qt dialog (gold title, mascot, scrollable HELP_TEXT body, "Got it" close). Same content the CTk app shipped, pulled from the shared logic shim so both UIs stay in sync. Previously a `print()` placeholder.
- **Compare per-mod file drill-down** — every mismatched mod in the Compare results is now a collapsible card. Click the header to expand and see:
  - Recommended action banner (specific to that mod's mismatch shape)
  - "Loose/junk files causing this diff" warning when applicable (dev artifacts like `.git/`, user junk like `Thumbs.db`)
  - Every differing file with its kind marker (`− only yours`, `+ only theirs`, `~ differs`), impact-classification emoji + label (script / UI / loc / cosmetic / metadata / other), full path, and size-detail
  - Files sorted by impact (high → none) and then alphabetically
  - Header always shows the impact verdict, category breakdown, and version mismatch warning when applicable

### Changed
- **Slim PyInstaller bundle.** Excluded ~50 Qt modules NullSync doesn't use — QtWebEngine (~75 MB), Qt3D (~20 MB), QtQuick / QtQml (~30 MB), QtMultimedia (~15 MB), plus QtCharts, QtPdf, QtNetwork, QtSql, QtSvg, QtOpenGL, QtNfc, QtBluetooth, QtPositioning, QtLocation, QtSerialPort, QtTextToSpeech, QtPrintSupport, and a handful of others. Final exe is **73 MB** vs v2.0.1's 275 MB. **NullSync only uses QtCore + QtGui + QtWidgets.**
- The `logic.py` shim now finds `stellaris_sync.py` correctly when running from a PyInstaller bundle (via `sys._MEIPASS`) as well as from a dev source tree. Single change but it's what made the slim build runnable.

## v2.0.1 (2026-05-16)

**TOS dialog + startup splash.**

- **Terms of Service prompt is back.** v2.0.0 launched directly into the main window without re-checking the saved `tos_agreed_version`. v2.0.1 fires the same TOS check the CTk app did: if your saved version is below the current `TOS_VERSION` (which bumped to 2 when the heartbeat disclosure was added), you get re-prompted on launch. Decline cleanly exits the app; accept saves the new version and continues. Built as a real Qt dialog with a scrollable read-only body and gold-bordered accept / decline buttons.
- **Startup splash overlay.** Brand wordmark + BETA pill + tagline hold at full opacity for 2.5 seconds, then fade to zero over 1 second using a real `QPropertyAnimation` on opacity — direct port of the Nullcore Companion's `MainWindow.xaml` splash animation. Eats clicks while visible so a user can't fight the fade by clicking through to the main window. Auto-hides after fade.

## v2.0.0 (2026-05-16)

**Full UI rewrite in PySide6 / Qt.** The v1.4.x line in CustomTkinter couldn't reach the visual quality of the rest of the Nullcore product family — flat widget rendering with no gradient brushes, no widget transparency, no real drop shadows. v2.0.0 is a from-scratch UI built in Qt that finally has the polish we've been chasing.

### Visual overhaul
- **Borderless window** with custom title bar (drag, double-click maximize, min/max/close buttons that glow gold on hover).
- **Windows 11 acrylic backdrop** — the desktop subtly blurs through the app, with a semi-transparent gradient + diagonal stripe layer painted over it.
- **Continuously animated diagonal gold stripes** running across the entire window background. CTk couldn't do this; Qt's painting model handles it natively.
- **NULLSYNC wordmark** painted with a vertical gold gradient (light → standard → deep gold) plus a soft gold drop-shadow glow. **BETA badge** with its own subtle shadow next to it.
- **Gold gradient divider** under the banner, fading in from edges and peaking center.
- **Content card** wrapping the tab area — rounded corners, semi-transparent dark fill, drop shadow, gold-dim border edge.
- **Themed tab strip** — gold accent on the selected tab, warm-amber hover on others. No more blue leakage from CTk's dark-blue preset.
- **All standard controls themed** end-to-end: buttons, inputs, checkboxes, dropdowns, scrollbars, progress bars, switches.

### Functional parity (mostly)
- **Fingerprint tab** — full port. Scan, progress bar, results table, save fingerprint file, quick share code, sync checksum display with copy button.
- **Compare tab** — core port. Two-panel "Yours" / "Theirs" loaders (file OR pasted share code), Compare button, checksum match/mismatch verdict, impact-ranked diff sections (mods you have, mods they have, mods that differ, load order, DLC). Per-mod file-level drill-down (the largest sub-panel in the CTk version) is deferred to v2.0.1.
- **Diagnose tab** — full port. Background-threaded Run Checks pipeline, color-coded result rows for all check categories.
- **Settings tab** — full port. Theme picker (with premium gate), update-check toggle (gates both update check and heartbeat).
- **License tab** — full port. Activation form, status display, deactivate flow.
- **About tab** — full port. Hero card, early-version notice, looking-for-testers card, community links, bug-report tools, license/privacy info.

### Under the hood
- Business logic (mod scanning, fingerprint generation, checksum compute, Steam discovery, share-code encode/decode) lives in the existing `stellaris_sync.py` module and is re-exported via a `logic.py` shim. Both UI codebases (the legacy CTk and the new Qt one) call the same underlying functions, so any fingerprint produced by v1.4.x compares perfectly against one produced by v2.0.0.
- Heartbeat / TOS / settings persistence carries over from v1.4.x — your saved theme, license key, Stellaris folder, and TOS-agreed flag transfer cleanly.
- File size is ~275 MB (vs ~38 MB on v1.4.x). Qt's bundle is heavier than CustomTkinter's. v2.0.1 will trim by excluding unused Qt modules (QtWebEngine, etc.).

### Migration
- Existing v1.4.x users: the in-app update banner will point you at this release. Download `NullSync.exe`, drop it next to (or replace) your existing one, launch. Your settings carry over.
- The CustomTkinter v1.4.x build is retired. Source stays in git history for reference, but the v2.x line is the active codebase going forward.

## v1.4.2 (2026-05-16)

**More theme polish.**

- **Killed the blue hover leakage on tabs and buttons.** v1.4.1 patched CTk's default `fg_color` and `hover_color`, but tab strips use additional theme keys (`selected_color`, `selected_hover_color`, `unselected_hover_color`, plus CTkTabview's `segmented_button_*` variants) that were still serving the original dark-blue preset. Now all of them get a Nullcore-palette color, so hovering anywhere gives you a warm-amber tint instead of a blue glow.
- **BETA badge** next to the NULLSYNC title — small gold pill, dark warm fill, matches the brand identity of the rest of the banner. Signals to first-time users that the project is still iterating.
- Scrollbars, scrollable frames, text boxes, dropdown menus, switches, checkboxes, sliders, progress bars, and inputs all now consistently themed (previously a few stragglers were still blue-tinted).

## v1.4.1 (2026-05-16)

**Nullcore theme polish pass.** Visual fixes for issues that landed with v1.4.0:

- **Glass effect** now actually applies on Windows 11. v1.4.0 fired the DWM call before the window's HWND was fully realized, so it silently no-op'd. Deferred to 250ms after window mapping.
- **Stripes are now visible.** v1.4.0 had them rendering behind everything, but CTk's opaque widget backgrounds hid them. Now the banner has the diagonal stripes baked directly into its background image (PIL-rendered gradient + stripes + soft gold accent line along the bottom), with a slow pan animation. Stripes also still render in the window margins via the background canvas.
- **Gold reads as gold, not yellow.** Shifted the accent tone from `#D4AF37` (companion's literal hex) to `#CFA53D` (slightly warmer/richer). The companion has WPF gradient brushes and drop shadows that lift `#D4AF37` into looking metallic — CTk's flat fill rendering needs a slightly warmer base to compensate.

## v1.4.0 (2026-05-16)

**Nullcore theme + anonymous install telemetry.**

### Visual overhaul
- New default theme **"Nullcore"** — gold-on-black palette pulled directly from the companion app, for visual consistency across the Nullcore product family. Existing themes (Sakura, Cobalt, Midnight) untouched and still selectable in Settings.
- Animated diagonal gold-tinted stripes pan continuously behind the UI (theme-coordinated, runs at ~30fps).
- Stylized **NULLSYNC** wordmark in the banner — vertical gold gradient with a soft ambient glow underneath, rendered at runtime via PIL using Constantia (with Cambria/Georgia fallbacks).
- Gold horizontal divider sits under the banner — fades in from the edges, peaks at the center.
- Help button + subtitle now obey the active theme (previously hardcoded pink leftovers showed through on non-Sakura themes).
- **Windows 11 acrylic glass backdrop** is now on by default for the Nullcore theme without needing a premium activation or a manual toggle. Other themes still respect the existing premium gate.

### Analytics — anonymous install heartbeat
- On startup, the app now sends an anonymous "I exist" heartbeat to `https://license.rankup.lol/heartbeat` so the project can count unique installs versus simple GitHub download totals (which can't tell new users from existing users re-downloading after an update banner).
- The only data sent is: a **SHA256 hash** of your machine ID (the raw identifier never leaves your computer — it's hashed locally first), the product name "NullSync", and the version number.
- Sent **at most once per 24 hours** (throttled via a timestamp in settings.json).
- Gated by the same single **"Check for updates on startup"** toggle that controls the GitHub update check. Untick it in Settings and both go off.
- Updated TOS (TOS_VERSION = 2) describes the heartbeat explicitly — existing users will be re-prompted to agree on first launch of this version.

## v1.3.7 (2026-05-13)

- Added a "looking for testers" card to the startup splash and a permanent matching card on the About tab. NullSync is early and there's a lot of polishing still to do; invites users who'd like to help test new features, give feedback, and play co-op Stellaris sessions to test mods against real multiplayer to hop into the Discord.
- Added a short matching section to the GitHub README so the recruiting message reaches people browsing the repo too.

## v1.3.6 (2026-05-13)

**Clarity pass — plain English over jargon**

- Compare results now tell you **who** needs to update when a mod's version doesn't match. NullSync parses both version strings and names the player who's behind ("You need to update this mod" vs "Your friend needs to update this mod"), instead of the old generic "Update mismatch — one of you should update".
- Every fix suggestion in the Compare tab is now a plain action item: "You need to reinstall this mod" / "Your friend has junk files in this mod's folder" / "Both of you need to reinstall this mod" — instead of headers like "Theirs is missing files" or "Local edits or partial update".
- Reinstall instructions are now spelled out ("In Steam, right-click the mod → Unsubscribe → Subscribe again") instead of leaving the user to figure out "unsubscribe + resubscribe".
- Section headers reworded across the board: "In YOUR fingerprint, not theirs" → "Mods you have that your friend doesn't"; "Load Order Mismatch (real Stellaris checksum cares about this)" → "Your mod load order doesn't match"; etc.
- Verdict labels swapped from checksum-speak to outcome-speak: "Likely cause of checksum mismatch" → "This will stop you connecting in multiplayer". The word "checksum" is mostly gone from user-facing messages — replaced with what the user actually cares about (whether they'll connect).
- Mod load health section now explains in plain terms why files can match but the game still rejects multiplayer, and points directly at which mod to reinstall.

## v1.3.5 (2026-05-13)

**Stability + diagnostics pass**

- Added a rotating activity log at `%APPDATA%\NullSync\logs\nullsync.log`. Records scans, compares, diagnose runs, and recoverable errors. Sanitized (no usernames, no share codes, no license keys) so it's safe to share for bug reports.
- Added a crash log at `%APPDATA%\NullSync\logs\crash.log`. Only written when the app hits an unexpected error. Catches both background-thread crashes and Tk callback exceptions; surfaces a friendly notice so the user knows what happened.
- New buttons in About > Bug Reports: **Open Log Folder** and **Copy Diagnostic Info**. The latter copies version, platform, and the last ~80 sanitized log lines straight to the clipboard for pasting into Discord or GitHub issues.
- A single broken mod in your playset no longer kills the whole scan. Per-mod errors are caught, logged, and the offending mod is added to the "skipped" list with a reason instead.
- error.log reader now caps reads at 5 MB (tail) so users with months-old installs don't pay the cost of parsing a massive log file.
- Workshop base path lookup is now cached. Eliminates a few thousand redundant filesystem checks on large mod lists.
- File hashing now uses 1 MB chunks (was 64 KB) and tracks total size inline. Modest scan speedup on big mods.
- `fingerprint_mod` switched from `pathlib.Path` allocations to string paths in its inner loop, reducing per-file overhead on mods with thousands of files.

## v1.3.4 (2026-05-13)

- Added an "early version" notice to the startup splash and a matching permanent card on the About tab. Asks users to report rough edges, confusion, or bugs in the Discord or on GitHub so the next releases can sand them down.

## v1.3.3 (2026-05-13)

- Renamed the user-facing "predicted checksum" to **sync checksum** throughout the app and documentation. The previous wording implied NullSync was trying to predict Stellaris's internal checksum algorithm. What NullSync actually does is generate its own deterministic checksum from your setup - if two players see the same value, their setups are compatible and the game will accept them together. The new name reflects that.

## v1.3.2 (2026-05-13)

- Added an in-development teaser row to the startup splash. Points to an upcoming Stellaris mod focused on fleets and how they handle losing ships.

## v1.3.1 (2026-05-13)

First public release.

**Core features**

- Fingerprints your active Stellaris mod setup: load order, file integrity, descriptor info, sync checksum
- Shareable codes for quickly comparing setups with a friend over chat
- Side-by-side compare with mismatch attribution, version detection, file-level differences, and missing-dependency surfacing
- Diagnose tab: identifies broken Workshop subscriptions, mods with critical script errors in error.log, and missing dependencies

**App experience**

- About tab with project info, community links, and credits
- License tab for future premium activation. The activation service is being rolled out; in the meantime every user is on the free tier and the Activate button stores entered keys locally only
- Sakura theme (free), plus Cobalt and Midnight as premium-tier themes
- Windows 11 Acrylic glass effect as a premium-tier visual option
- Terms of Service prompt on first launch (versioned so future updates can re-prompt)
- Brief welcome panel on every launch for free-tier users: thank-you note, Discord and GitHub links, and a list of my published Stellaris Workshop mods. Premium users skip it entirely
- On-startup update notifier that checks the public GitHub Releases API and shows a dismissible banner when a new version is available. Can be turned off in Settings
