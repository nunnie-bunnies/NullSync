# NullSync

A Windows desktop tool for diagnosing Stellaris multiplayer mod mismatches.

When you and a friend can't connect because of a checksum mismatch, NullSync compares your mod setups and tells you what's actually different. It works even when one of you has a mod that "looks installed" in the launcher but silently failed to load.

## Features

- Fingerprints your active Stellaris mod setup (load order, file hashes, descriptors)
- Generates a small share code you can send to a friend over Discord
- Compares two fingerprints side-by-side and explains what's mismatched and why
- Diagnoses common problems: broken Workshop subscriptions, mods with script errors, missing dependencies
- Predicts what the in-game checksum will be before you launch
- Three themes (Sakura, Cobalt, Midnight) and Windows 11 Acrylic glass effect

## Install

1. Grab the latest `NullSync.exe` from the [Releases page](../../releases/latest).
2. Run it. No installer, no admin rights needed.
3. The app stores its settings in `%APPDATA%\NullSync\`.

NullSync checks GitHub for new versions on startup and shows a banner if one is available. You can turn this off in Settings.

## How to use it

**Quick start with a friend:**

1. Both of you run NullSync, click **Scan** on the Fingerprint tab.
2. One of you clicks **Share Code**, copies the result, sends it over Discord.
3. The other pastes it on the Compare tab. NullSync tells you what differs.

**Diagnose your own setup:**

The Diagnose tab runs a series of checks and points out misconfigured mods, broken subscriptions, and anything Stellaris is logging errors about.

## System requirements

- Windows 10 or 11 (64-bit)
- Stellaris installed via Steam
- ~80 MB free disk

## Reporting issues

Use the [Issues tab](../../issues) for bugs and feature requests. Include:

- Your NullSync version (Settings tab > About)
- What you were doing when it broke
- Any error message shown
- Your Stellaris game version

## License

All rights reserved. See [LICENSE](LICENSE).

The compiled binary is free to download and use for personal Stellaris play. Redistribution, reverse engineering, and modification are not permitted.

---

**NullSync** - A Nullcore Product - by Nunnie Bunnies (Mao Mao)
