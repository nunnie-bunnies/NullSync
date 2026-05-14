# Changelog

## v1.3.2 (2026-05-13)

- Added an in-development teaser row to the startup splash. Points to an upcoming Stellaris mod focused on fleets and how they handle losing ships.

## v1.3.1 (2026-05-13)

First public release.

**Core features**

- Fingerprints your active Stellaris mod setup: load order, file integrity, descriptor info, predicted in-game checksum
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
