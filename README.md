# Music Manager — Releases

This repository hosts the signed Windows installers for **Music Manager**, a desktop tag-management tool for keeping a personal music collection clean and consistently organized.

The application source code is maintained privately by BoxSoft Corporation; this repository contains only the published release artifacts that the in-app updater downloads.

---

## Download

Grab the latest installer from the [**Releases page**](https://github.com/BoxSoft/MusicManager-releases/releases/latest).

The release assets you'll see for each version:

| Asset                                  | What it is                                                              |
|----------------------------------------|-------------------------------------------------------------------------|
| `Music Manager Setup <version>.exe`    | The NSIS installer. Download and run this.                              |
| `Music Manager Setup <version>.exe.blockmap` | Used by the in-app updater for differential downloads. Do not download manually. |
| `latest.yml`                           | Update manifest read by installed copies. Do not download manually.     |

### System requirements

- Windows 10 or 11, 64-bit
- Your music library (the folder you want to manage)

### Install

1. Download `Music Manager Setup <version>.exe`.
2. Run it. The installer is signed by **BoxSoft Corporation** via Microsoft Trusted Signing.
3. The installer is per-user (no admin elevation required) and lets you pick the install location. Start Menu and desktop shortcuts are created automatically.

### Where your data lives

User data — settings, the keep-caps allowlist, the aliases file, etc. — lives under:

```
%APPDATA%\Music Manager\Settings\
```

This is outside the install folder, so reinstalling or upgrading **never touches your data**. Uninstalling removes the application but leaves this folder in place; delete it manually if you want a clean slate.

---

## What Music Manager does

Music Manager edits the tags inside your audio files and the folders around them. It is not a player and does not stream. The opinionated take is that the folder structure and the tags should agree, both should follow consistent conventions, and the app should be loud about it when they don't.

Typical things it handles:

- Inconsistent capitalization across track titles, with a learnable "keep these as-is" allowlist
- Straight quotes / curly quotes / verbose classical naming
- Track-numbering problems — missing numbers, gaps, or duplicates — with one-click renumbering
- Missing or inconsistent tags (genre, year, album name, composer) across an album
- Album folders that have drifted from the album-artist subfolder they belong under, or folder names that need tidying (stray leading articles, `[YYYY]` prefixes)
- Duplicates: same album imported twice, scattered across artist folders, or sharing a tag with a different folder
- A proactive **Cleanup scan** that flags every problem type across the library, with per-problem filters to work through them and per-album exemptions to silence the false positives
- An "Intake → fix → move to Library" workflow that keeps fresh rips and downloads out of the canonical collection until you've verified them
- ReplayGain tagging via `rsgain`
- Auto-lookup of album art and metadata from common sources (AllMusic, MusicBrainz, Discogs, iTunes, Amazon, Bandcamp)

Supported audio file extensions: `.flac`, `.mp3`, `.wav`, `.m4a`, `.m4b`, `.m4p`, `.aac`, `.ogg`, `.oga`, `.opus`, `.aif`, `.aiff`, `.wma`, `.ape`, `.wv`, `.dsf`, `.dff`.

---

## Automatic updates

Installed copies check for new versions on startup (about five seconds after launch) and again whenever you click **Check for Updates** in `Settings → About`.

When a newer version is available:

1. A top-of-app banner appears: "A new version (v…) is available — downloading…"
2. The download runs in the background; the banner shows percent progress.
3. When the download completes and the SHA-512 hash verifies, the banner switches to "Update v… downloaded — restart to apply." with a **Restart and Install** button.
4. Clicking restart exits the app, runs the installer over the existing install, and relaunches the new version. Your data is untouched.

There is no telemetry beyond the update check itself, which is a single HTTPS request to this repository for the `latest.yml` manifest.

---

## Reporting issues

Bug reports and feature requests can be filed on the [Issues tab](https://github.com/BoxSoft/MusicManager-releases/issues) of this repository.

When filing a bug, please include:

- The version you're running (visible in `Settings → About`).
- Windows version.
- Steps to reproduce, or a screenshot showing the unexpected state.
- For tag-related bugs, the file extension and (if possible) the offending tag values.

---

## License & ownership

Music Manager is © BoxSoft Corporation. The installer is provided as-is for personal use; redistribution of the binaries is not authorized without permission.

The source code is maintained in a private repository. This releases repository exists solely to host the signed artifacts and update manifest that the in-app auto-updater consumes.
