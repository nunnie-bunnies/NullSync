# Changelog

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
