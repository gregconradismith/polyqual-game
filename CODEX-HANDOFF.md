# PolyQual Game Codex Handoff

Date: 2026-06-18

## Repository

Local repo on this machine:

```text
/Users/greg/Library/CloudStorage/Dropbox/Main/Git/polyqual-game
```

GitHub repo:

```text
git@github.com:gregconradismith/polyqual-game.git
https://github.com/gregconradismith/polyqual-game
```

Live GitHub Pages app:

```text
https://gregconradismith.github.io/polyqual-game/
```

## Current Git State

Branch:

- `main`: production branch used by GitHub Pages.

Remote tracking:

- `main` tracks `origin/main`.
- At this handoff, local `main` and `origin/main` are both at `69e805b`.

Recent commits:

```text
69e805b Document live app URL
cfb83a9 Add sound effects toggle
f47701e Add handoff notes
8f60f0c Merge pull request #1 from gregconradismith/upgrade
1e08d27 Upgrade scoring feedback
```

Current working tree at handoff:

```text
Clean before adding this CODEX-HANDOFF.md file.
```

Note: `.gitignore` now ignores `.DS_Store`.

## What The App Is

This is a MATLAB-free static web app version of the original `polyqualgame.m`
idea. It runs directly from GitHub Pages and can be added to an iPhone Home
Screen from Safari.

Important files:

- `index.html`: app shell and PWA/iPhone metadata.
- `styles.css`: responsive styling.
- `app.js`: polynomial generation, qualitative comparison, scoring, canvas
  drawing, answer flow, and sound effects.
- `manifest.webmanifest`: PWA manifest.
- `service-worker.js`: offline/app-shell cache.
- `icons/`: app icons.
- `polyqualgame.m`: original MATLAB reference script retained in the repo.
- `README.md`: user-facing project notes, including the live URL.
- `.gitignore`: ignores `.DS_Store`.

## Current Features

- Generates two related polynomial curves.
- Asks whether the curves are qualitatively similar.
- Supports comparing signs of `f'` and `f''`, with optional inclusion of `f`.
- Shows a reveal/answer-key view after answering.
- Tracks running score, accuracy, current streak, and best streak.
- Shows recent round history.
- Plays correct/incorrect sound effects through Web Audio.
- Includes a Sound effects toggle; the preference is saved in the browser.
- Includes a Show zero line toggle.
- Works as a static PWA with service-worker caching.

## Most Recent Changes

`cfb83a9 Add sound effects toggle`:

- Added a Sound effects checkbox to the controls.
- Persisted the sound preference in `localStorage`.
- Gated Web Audio playback behind the saved preference.
- Bumped the service-worker cache from `polyqual-game-v2` to
  `polyqual-game-v3`.
- Documented the sound toggle in `README.md`.

`69e805b Document live app URL`:

- Added the live GitHub Pages URL to `README.md`.
- Added `.gitignore` with `.DS_Store`.

## Validation Already Run

For the sound-toggle work:

```sh
node --check app.js
node --check service-worker.js
git diff --check
```

Browser smoke checks were also run against local preview:

- Sound toggle persisted after reload.
- Answering a round revealed the feedback panel and updated score.
- No console errors.
- No horizontal overflow at desktop width.
- No horizontal overflow at a mobile viewport.

For `.gitignore`:

```sh
git check-ignore -v .DS_Store
```

## Deployment Notes

GitHub Pages is configured from:

```text
Branch: main
Folder: / (root)
```

The live app is:

```text
https://gregconradismith.github.io/polyqual-game/
```

If an older UI appears on a browser or iPhone, it is probably a previous
service-worker cache. Reload once, close/reopen the app, or use a cache-busted
URL such as:

```text
https://gregconradismith.github.io/polyqual-game/?cache-bust=2026-06-18
```

## Continuing On Another Computer

Clone and inspect:

```sh
git clone git@github.com:gregconradismith/polyqual-game.git
cd polyqual-game
git branch -a
git status
git log --oneline --decorate -5
```

Start from production:

```sh
git switch main
git pull
```

Preview locally:

```sh
python3 -m http.server 8765
```

Then open:

```text
http://127.0.0.1:8765/
```

Basic checks after editing:

```sh
node --check app.js
node --check service-worker.js
git diff --check
```

## Suggested Next Improvements

- Add a timed mode.
- Add streak milestone display or celebratory streak badges.
- Add a short explanatory/about modal for students.
- Add deterministic seed mode for preparing classroom examples.
- Consider moving `polyqualgame.m` into a `reference/` folder if the repo should
  be purely web-app facing.
- Consider adding a tiny in-app version/cache label while testing service-worker
  updates.
