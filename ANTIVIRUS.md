# Antivirus and SmartScreen notices

Short version: NullSync is safe. It is a small, compiled desktop app that is not
code-signed, and that combination sometimes makes antivirus software show a
generic warning. This page explains why that happens, how to confirm it for
yourself, and what to do about it.

If you ever do not trust a download, do not run it. The guidance below is here so
you can make an informed decision, not to talk you past your own judgment.

---

## Tested on an aggressive antivirus setup

I build and test NullSync on a machine running one of the more aggressive antivirus
products available, the kind that flags far more than the average scanner. The
current installer build installs and runs on it with no warning at all. The older
single-file build was the one that occasionally tripped its heuristics, which is a
big part of why NullSync now ships as an installer. So the most cautious setup I
have on hand is happy with the version you are downloading.

---

## Why this happens

NullSync is written in Python and compiled into a native Windows binary. A few
ordinary properties of that kind of build push antivirus heuristics to guess
"suspicious," even though nothing harmful is present:

- **It is not code-signed.** Code-signing certificates cost money every year, which
  is hard to justify for a free hobby tool. Unsigned binaries from a small
  publisher are treated with suspicion by default. To be straight about it:
  NullSync is free and built to help people, so I am not going to pay for a yearly
  certificate just to quiet a few warnings. The occasional flag is the trade-off,
  and I would rather keep the tool free than spend money making it look official.
- **It bundles a runtime.** The download is large because it packs everything it
  needs to run into the install, so you do not have to install Python or anything
  else. Generic scanners sometimes treat "large unfamiliar binary that bundles a
  runtime" as a red flag on its own.
- **Heuristic, not signature, detections.** The warnings are almost always generic
  machine-learning verdicts with names like `Gen:Variant.*`, `Gen:Heur.*`,
  `ML.Attribute.HighConfidence`, `Trojan.Generic`, or similar. A name starting
  with `Gen:` or `Heur` means the scanner did not match a known threat. It made a
  statistical guess based on surface traits.

This is a well-documented, industry-wide problem with compiled Python apps, not
something specific to NullSync. See the references at the bottom.

### Example

One report against an early NullSync build was Bitdefender flagging a temporary
build file as `Gen:Variant.Giant.Lazy.4088`. The `Gen:Variant` prefix is the tell:
it is a generic heuristic guess, not a confirmed threat. Different antivirus
products will use different generic names for the same kind of false positive.

---

## How to verify it yourself

You do not have to take this page's word for it. Two quick checks:

1. **Look up the exact detection name.** Whatever your antivirus calls it (for
   example `Gen:Variant.Giant.Lazy.4088`), search for that name plus the words
   "false positive" and "PyInstaller" or "Nuitka". You will find the same generic
   detections reported against countless legitimate compiled-Python programs.

2. **Scan it on VirusTotal.** Upload the file to
   [virustotal.com](https://www.virustotal.com/). It runs the file past around 70
   antivirus engines at once. A genuine threat lights up most of them. A false
   positive typically shows only a handful of engines flagging it with generic
   heuristic names, while the major engines pass it. That pattern is the signature
   of a false positive, not malware.

---

## What NullSync actually does on your machine

- It reads your existing Stellaris files to compare mod setups. It does not modify
  your game, mods, saves, or any game state.
- It writes only its own settings under `%APPDATA%\NullSync\`.
- Its only outbound network calls are a check against GitHub's public release API
  for updates, and an anonymous once-a-day "install exists" count that sends just a
  hashed machine identifier, the app name, and the version. No personal data, no
  file contents. Both are tied to the "check for updates on startup" toggle in
  Settings, and the install count is deliberately delayed well after launch.

Full privacy detail is in the README and the License.

---

## How to allow it

If your antivirus quarantined or blocked NullSync and you have decided to run it:

- **Windows SmartScreen:** click **More info**, then **Run anyway**.
- **Most antivirus products:** restore the file from quarantine and add an
  exclusion for it. The exact steps vary by product, so check your antivirus's help
  for "restore from quarantine" and "add exclusion."

## Helping fix it for everyone

False positives get corrected when they are reported. If you want to help, you can
submit NullSync to your antivirus vendor as a false positive. Microsoft and most
major vendors have a submission form:

- Microsoft Defender: [submit a file for analysis](https://www.microsoft.com/en-us/wdsi/filesubmission)
- A community-maintained list of vendor false-positive submission links:
  [false-positive-malware-reporting](https://github.com/hankhank10/false-positive-malware-reporting)

---

## References

- [Antivirus false positives with PyInstaller executables](https://www.pythonguis.com/faq/problems-with-antivirus-software-and-pyinstaller/)
- [PyInstaller onefile flagged as a virus (project issue thread)](https://github.com/pyinstaller/pyinstaller/issues/6754)
- [VirusTotal](https://www.virustotal.com/)
