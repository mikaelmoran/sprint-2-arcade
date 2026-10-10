# GitHub Release Guide

This project is ready to publish as an English-language GitHub repository and
as a macOS release download.

## Recommended repository contents

Keep the source, tests, `README.md`, `screensaver/`, `game/`, and
`docs/screenshots/` in the repository. The ZIP file is best attached to a
GitHub Release rather than committed into the source tree.

The repository includes ten effect-gallery screenshots under
`docs/screenshots/`. GitHub renders the gallery directly in `README.md`.

Recommended release asset:

`dist/Sprint-2-Arcade-2.1-macOS-universal.zip`

It contains:

- `Sprint 2 Arcade.saver` — the universal Intel and Apple Silicon screen saver;
- `Sprint 2 Settings.app` — the Tahoe Options-button fallback;
- `README.md` — the English installation and troubleshooting guide.

## Create the repository

1. Create a new GitHub repository, for example `sprint-2-arcade`.
2. Keep the repository visibility and license choices appropriate for your
   project and distribution rights.
3. From the project directory, review the files before committing:

   ```bash
   git init
   git add README.md docs screensaver game main.py config.py requirements.txt tests
   git status
   git commit -m "Release Sprint 2 Arcade screen saver 2.1"
   git branch -M main
   git remote add origin https://github.com/YOUR-ACCOUNT/sprint-2-arcade.git
   git push -u origin main
   ```

Do not commit personal macOS build output, `.venv/`, signing certificates, or
private credentials. Add those paths to `.gitignore` if they are not already
ignored in your local setup.

## Create the GitHub Release

1. Open the repository on GitHub and choose **Releases → Draft a new release**.
2. Create the tag `v2.1.0`.
3. Use the title `Sprint 2 Arcade Screen Saver 2.1`.
4. Upload `dist/Sprint-2-Arcade-2.1-macOS-universal.zip` as the release asset.
5. Paste the release text below and publish the release.

### Suggested release text

```text
Sprint 2 Arcade Screen Saver 2.1

An English-language macOS screen saver inspired by Atari/Kee Games Sprint 2
(1976). The native module is universal for Intel and Apple Silicon Macs.

Highlights:
- fixed-screen overhead racing with four AI cars;
- twelve selectable reconstructed tracks;
- 40 optional visual effects;
- CRT curvature, scanlines, phosphor glow, trails, skid marks, signal noise,
  RGB edge split, sync tear, oil shimmer, collision flashes, and more;
- permanent but moving/fading JMR Development credit;
- separate settings app for the macOS Tahoe Options-button issue.

Installation:
1. Download and unzip the macOS universal ZIP.
2. Double-click `Sprint 2 Arcade.saver`.
3. Choose Sprint 2 Arcade in System Settings → Wallpaper → Screen Saver.
4. Open Options, select a preset, and press Save.

If Options does not open on macOS Tahoe, quit System Settings with Command-Q
and reopen it. If it still fails, double-click `Sprint 2 Settings.app` from
the unzipped release folder.

This build is locally signed but not notarized by Apple. macOS may ask the
user to approve the module in Privacy & Security.
```

## Verify a release before uploading

Run the native and Python tests from the project directory:

```bash
./screensaver/test_macos_saver.sh
.venv/bin/python -m pytest -q
unzip -t dist/Sprint-2-Arcade-2.1-macOS-universal.zip
```

The native test validates both architectures, signatures, settings controls,
all twelve tracks, AI recovery, and rendered previews. The Python suite covers
the game physics and scoring model.

## Important distribution note

This is an independent fan recreation. It does not include Atari ROM files,
original copyrighted artwork, or original audio recordings. The README
documents which behaviors are historically verified and which are deliberate
approximations. If you distribute the project publicly, review the repository
name, logos, screenshots, and license with your own legal/distribution policy.
