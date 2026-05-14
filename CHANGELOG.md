# Changelog

## v1.1.2 (2026-05-13)

- Reworded the mod-presence section in Compare results. "Mods only on YOUR/THEIR side" is now "In YOUR/THEIR fingerprint, not theirs/yours".
- Added an explanatory note above that section explaining the common case where a Workshop subscription silently fails (files missing, no thumbnail) - the affected player's launcher will look normal while their fingerprint correctly excludes the mod. Points users to the Diagnose tab for confirmation.

## v1.1.1 (2026-05-13)

Maintenance release. Verifies the in-app update notifier end-to-end.

## v1.1.0 (2026-05-13)

First public release.

- Mod fingerprinting with predicted checksum
- Share code generation (compact, base64+gzip)
- Side-by-side compare with mismatch attribution
- Diagnose tab: broken Workshop subscriptions, script errors, missing dependencies
- Three themes: Sakura, Cobalt, Midnight
- Windows 11 Acrylic glass effect (optional)
- On-startup update check via GitHub Releases API
