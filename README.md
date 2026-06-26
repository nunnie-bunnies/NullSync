# NullSync

NULLSYNC automatically detects Stellaris multiplayer incompatibilities including mod mismatches, load order conflicts, altered files, DLC differences, and desync risks

> A desktop tool for diagnosing Stellaris multiplayer mod mismatches.

When you and a friend can't connect because of a checksum mismatch, NullSync compares your mod setups and tells you what's actually different. It works even when one of you has a mod that "looks installed" in the launcher but silently failed to load.

[**Download the latest release**](https://github.com/nunnie-bunnies/NullSync/releases/latest)

---

## Why NullSync exists

If you've played heavily modded Stellaris multiplayer, you've probably experienced this:

- same mod list
- same load order
- same game version
- same DLC

…but the lobby still says:

> **"Game version differs."**

Then begins the ritual:

- Nervously screenshotting your mod list into Discord
- Unsubscribing and re-subscribing, one mod at a time
- Nudging the load order around blindly
- Nitpicking every checksum by hand
- Insisting the launcher restart three more times
- Eventually sacrificing an envoy to the checksum gods

NullSync exists to tell you exactly what's wrong instead of making you guess.​‌​​‌‌‌​​‌​​​​‌​​‌​​‌‌‌​​‌​‌​​‌‌

---

## Screenshots

**Fingerprint tab** - scan your mods, see your sync checksum and per-mod manifest.

![NullSync Fingerprint tab](screenshots/fingerprint.png)

**Compare tab** - paste your friend's share code, get a colour-coded breakdown of every difference: missing mods, content changes, load order mismatches.

![NullSync Compare tab](screenshots/compare.png)

**Diagnose tab** - one-click health audit of your Stellaris install. Finds broken Workshop subscriptions, mods with script errors in error.log, and other silent issues that ruin multiplayer.

![NullSync Diagnose tab](screenshots/diagnose.png)

---

## Features

- Fingerprints your active Stellaris mod setup (load order, file integrity, descriptor info)
- Generates a small share code you can send to a friend over Discord
- Compares two fingerprints side-by-side and explains every mismatch
- Generates a sync checksum from your setup - if yours matches your friend's, you'll connect
- Diagnose tab: catches broken Workshop subscriptions, mods with script errors, missing dependencies
- Crash Analyzer: point NullSync at a Stellaris crash and it names the mod most likely responsible, so you stop bisecting your modlist by hand
- Runs on **Windows and Linux** (64-bit)
- Customizable app theme
- Built-in update checker - notified when a new version ships

---

## Install

### Windows

1. Grab the `NullSync-Setup` installer from the [Releases page](https://github.com/nunnie-bunnies/NullSync/releases/latest)
2. Run it. It installs per-user, so no admin rights are needed
3. Launch NullSync from the Start menu (or the desktop shortcut if you chose one)
4. Settings persist to `%APPDATA%\NullSync\`

Windows SmartScreen or your antivirus may warn you about the unsigned installer. This is normal for small independent projects and does not mean anything is wrong. For SmartScreen, click **More info** then **Run anyway**. For why antivirus sometimes flags compiled apps like this, and how to verify it for yourself, see [ANTIVIRUS.md](ANTIVIRUS.md).

### Linux (x64)

1. Download `NullSync-linux-x64-<version>.tar.gz` from the [Releases page](https://github.com/nunnie-bunnies/NullSync/releases/latest)
2. Extract it: `tar -xzf NullSync-linux-x64-*.tar.gz`
3. Make the launcher executable: `chmod +x NullSync`
4. Run it: `./NullSync`
5. Settings persist to `~/NullSync/`

The Linux build is newer and less battle-tested than the Windows one. It looks for Stellaris in the usual native and Proton/Steam Play locations; if it can't find your install, use the **Browse** button to point it there manually, and please [open an issue](https://github.com/nunnie-bunnies/NullSync/issues) if a path is missing.

---

## Quick start

**With a friend who can't join your game:**

1. Both of you open NullSync and click **Scan** on the Fingerprint tab
2. One person clicks **Share Code**, copies the result, pastes it in Discord
3. The other person opens the Compare tab and pastes the code there
4. NullSync displays every difference along with an explanation of what's likely causing the mismatch

**Just want to check your own install:**

Open the Diagnose tab and click **Run All Checks**. It will surface anything obviously broken about your Stellaris mod setup, even before you try to join a game.

---

## How It Works

NullSync scans your Stellaris installation when you click Scan. It reads which mods are active, the order they load in, and metadata about each one. From that it produces two things:

- A deterministic sync checksum derived from your mod setup. The checksum has one useful property: if two players see the same checksum, their setups are byte-for-byte compatible and they will connect cleanly
- A shareable fingerprint code that captures enough to compare against a friend's setup, without exposing anything personal about your machine

When you paste a friend's code, NullSync aligns both setups and identifies what's different - missing mods, version mismatches, files that diverge between the two of you, mods that loaded for one player but errored for the other.

The Diagnose tab runs a series of health checks against your install: misconfigured mod paths, broken Workshop subscriptions, mods showing critical errors in the game's own log, missing dependencies.

NullSync is **read-only**. It does not modify your Stellaris files, save data, mod files, or any game state. It does not connect to your game, only to your local filesystem.

---

## FAQ

**Is NullSync safe to run?**

Yes. It reads from your existing Stellaris files and writes only its own settings to `%APPDATA%\NullSync\`. It does not touch game files, mod files, saves, or anything outside its own settings folder.

**Does it phone home or collect any data about me?**

No usage data, no file contents, no analytics. The app does two small outbound calls on startup: one to GitHub's public release API to check for a new version, and one anonymous "I exist" heartbeat (sent at most once every 24 hours) so the project can count unique installs. The heartbeat sends only a hashed machine ID, the product name, and the version, with no name, no email, and no file paths. Both calls are gated by the same **Check for updates on startup** toggle in Settings; untick it and both stop.

**Why is the download fairly large?**

NullSync bundles its own runtime so you do not have to install anything else. The Windows installer is around 50 MB and expands to roughly 160 MB installed; the Linux archive is around 40 MB. Most of that is the bundled runtime and UI libraries, not NullSync itself.

**Do I need anything else installed?**

No. NullSync is self-contained on both Windows and Linux - no separate runtime to install.

**Will it work on Linux or Mac?**

Linux: yes, there's a native 64-bit Linux build (see the Install section). It's newer than the Windows build, so expect a few more rough edges. Mac: not currently.

**Windows SmartScreen or my antivirus flagged the download. Is it malware?**

No. NullSync is not code-signed (code signing certs are expensive for small indie projects), and compiled apps that bundle a runtime commonly trip generic antivirus heuristics. This is a known, industry-wide false positive, not a real detection. The full explanation, how to confirm it on VirusTotal, and how to allow it are in [ANTIVIRUS.md](ANTIVIRUS.md).

**Does NullSync support Stellaris with ironman or achievements enabled?**

NullSync is read-only and runs outside the game, so it has no effect on achievement eligibility.

**Will using NullSync change my Stellaris checksum?**

No. NullSync does not modify anything in your Stellaris folder. NullSync computes its own sync checksum from your setup, independent of Stellaris. Matching sync checksums between players means the underlying setups are identical, so the game will accept them together.

**My friend's share code is huge. Did I get it wrong?**

Share codes for normal mod lists fit easily in a Discord message. If the code is suspiciously long, you may have copied a full fingerprint JSON file instead. Use the **Share Code** button to generate the compact form.

**Can I use it to fingerprint a server, sync entire playsets, or push mods to my friend?**

No. NullSync is strictly a diagnostic tool. It doesn't transfer or install mods; that part still happens through the Paradox Launcher and Steam Workshop.

**Is this open source?**

No, NullSync is closed source. See [Source Code](#source-code) below.

---

## Troubleshooting

**"Stellaris directory not found"**

NullSync looks in standard locations under your Documents folder. If you've never launched Stellaris before, the directory won't exist yet. Run Stellaris once (even just to the main menu) so it creates the user folder, then try again. If you have Documents redirected to OneDrive or a custom location, use the **Browse** button to point NullSync at it manually.

**"No mods detected" / "Zero enabled mods"**

This usually means `dlc_load.json` is empty. Fix:

1. Open the Paradox Launcher
2. Activate your playset (or create one and add mods to it)
3. Click **Play** in the launcher - you can immediately quit once Stellaris is loading
4. This step is what tells the launcher to write your active mods to disk

Then re-run NullSync.

**Your sync checksums match, but Stellaris still won't let you connect**

Check the **Mod Load Health** section of the compare result. If a mod's files match between both players but it's failing to load on one side (script errors, missing dependencies), the in-game checksum will mismatch even when files are identical. NullSync flags this with a warning.

The fix is usually for the affected player to unsubscribe + re-subscribe to the broken mod, or to remove the mod from both playsets.

**The update banner says a new version is available, but I just downloaded NullSync**

Settings > About shows the version you're actually running. If it does not match the latest release tag, your download is stale. If versions match, your browser may have cached an older release page - refresh.

**The app refuses to launch / crashes on startup**

Common causes:

1. Antivirus quarantined part of the install. This is a known false positive on compiled apps; see [ANTIVIRUS.md](ANTIVIRUS.md) for why and how to allow it
2. The settings file is corrupted (`%APPDATA%\NullSync\settings.json` on Windows, `~/NullSync/settings.json` on Linux). Delete it and relaunch
3. A partial or interrupted install. Reinstall from a fresh download

If none of these help, open an [issue](https://github.com/nunnie-bunnies/NullSync/issues) with the steps to reproduce.

---

## Source Code

NullSync is closed source. Only the compiled binary is distributed.

GitHub automatically attaches "Source code (zip)" and "Source code (tar.gz)" archives to every release - these are auto-generated from this repository and **only contain documentation files** (README, LICENSE, CHANGELOG, ANTIVIRUS). They do not contain the application source.

---

## Antivirus and SmartScreen

NullSync is a compiled, unsigned app, so antivirus or SmartScreen may show a generic warning even though nothing is wrong. This is a common false positive for this kind of software. For the full explanation, how to confirm it for yourself on VirusTotal, and how to allow it, see [ANTIVIRUS.md](ANTIVIRUS.md).

For the record: NullSync is free and made to help people, so I am not going to pay for a yearly code-signing certificate just to quiet those warnings. It is unsigned because signing costs money, not because anything is wrong with it.

---

## System requirements

- Windows 10 or 11 (64-bit), or a 64-bit Linux desktop
- Stellaris installed via Steam (native or Proton/Steam Play on Linux)
- ~160 MB free disk
- Internet connection on startup if update checks are enabled (optional)

---

## Reporting issues

Use the [Issues tab](https://github.com/nunnie-bunnies/NullSync/issues) for bugs and feature requests. Include:

- Your NullSync version (Settings > About)
- Steps to reproduce
- What you expected vs what happened
- Your Stellaris version (Paradox Launcher shows it on the right)
- Any error message NullSync displayed

---

## Helping out

NullSync is early and there's a lot still being smoothed over. If you'd like to help test new features before they ship, give feedback on rough edges, or play co-op Stellaris sessions to validate mod setups against real multiplayer, hop into the [Discord](https://discord.gg/DRXRnPDmbJ) and say hi. No prior experience needed.

---

## Support & Premium

NullSync is free, and the core stays free, including the Crash Analyzer.

**NullSync Premium** is a web dashboard at [sync.nullcorestudio.com](https://sync.nullcorestudio.com) for keeping a whole group in sync:

- **Group rooms** - one page showing who in your crew is out of sync, before you start a game
- **Version-watch** - get told when a mod your group uses updates and will desync you
- **Fix-it plans** - not just what differs, but exactly what each person should do to match
- **Discord alerts** - a ping in your server when a mod updates
- **One-shot compare links** - send a friend a link, you both upload, see the diff, no pasting codes

Premium comes with supporting NullSync on [Patreon](https://www.patreon.com/nunniebunnie). Sign in at [sync.nullcorestudio.com](https://sync.nullcorestudio.com), connect your Patreon, and you're in. Supporting the project is entirely optional and hugely appreciated.

---

## License

All rights reserved. See [LICENSE](LICENSE) for full terms.

Free to download and use for personal Stellaris play. Redistribution, reverse engineering, and modification are not permitted.

---

**NullSync** - A Nullcore Product - by Nunnie Bunnies (Mao Mao)
