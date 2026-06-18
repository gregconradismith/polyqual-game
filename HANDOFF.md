# PolyQual Game Handoff

Date: 2026-06-18

## Repository

Local repo on this machine:

```text
/Users/gregconradismith/Main/Git/polyqual-game
```

GitHub repo:

```text
git@github.com:gregconradismith/polyqual-game.git
https://github.com/gregconradismith/polyqual-game
```

Live GitHub Pages site:

```text
https://gregconradismith.github.io/polyqual-game/
```

## Current Git State

Branches:

- `main`: production branch used by GitHub Pages. Includes the merged scoring/feedback upgrade.
- `upgrade`: feature branch that introduced the scoring/feedback upgrade; merged into `main` via PR #1.

Important commits:

- `2159850 first commit`: original GitHub Pages web app.
- `1e08d27 Upgrade scoring feedback`: scoring/feedback upgrade commit.
- `8f60f0c Merge pull request #1 from gregconradismith/upgrade`: merge commit on `main`.

At the time of this handoff, the local checkout was moved back to `main`, fast-forwarded to `origin/main`, and this `HANDOFF.md` file was being added for the computer move.

## What Was Built

The MATLAB script was converted into a MATLAB-free static web app:

- `index.html`: app shell and PWA/iPhone metadata.
- `styles.css`: responsive app styling.
- `app.js`: polynomial generation, qualitative comparison, scoring, canvas drawing, answer flow, and sound cues.
- `manifest.webmanifest`: PWA manifest.
- `service-worker.js`: offline/app-shell cache.
- `icons/`: app icons.
- `polyqualgame.m`: original MATLAB reference script, retained in the repo.

## Upgrade Branch Changes

The merged upgrade adds:

- Running score card with accuracy, correct count, attempts, current streak, and best streak.
- Top-bar streak indicator.
- Larger animated correct/incorrect verdict panel.
- Web Audio chime for correct answers and lower tone for incorrect answers.
- Service-worker cache bumped from `polyqual-game-v1` to `polyqual-game-v2`.

Verified locally before pushing:

- `node --check app.js` passed.
- `node --check service-worker.js` passed.
- Correct answer flow updates score/streak and large feedback.
- Incorrect answer flow resets streak and shows large feedback.
- Mobile-width layout has no horizontal overflow.

## Deployment Notes

GitHub Pages is configured from:

```text
Branch: main
Folder: / (root)
```

After merging `upgrade` into `main`, GitHub Pages deployed successfully. A cache-busted check showed the upgraded app live with the score card and streak UI. The standard URL is the one to use once the browser cache/service worker is refreshed.

If the old UI appears on a browser or iPhone, it is probably the previous service worker cache. Reload once, close/reopen the app, or use a cache-busted URL such as:

```text
https://gregconradismith.github.io/polyqual-game/?upgrade-check=1
```

## Continuing On Another Computer

Clone and inspect:

```sh
git clone git@github.com:gregconradismith/polyqual-game.git
cd polyqual-game
git branch -a
git status
```

Start from production unless you specifically need the old feature branch:

```sh
git switch main
git pull
```

The `upgrade` branch can still be checked out for comparison:

```sh
git switch upgrade
```

Preview locally:

```sh
python3 -m http.server 8765
```

Then open:

```text
http://127.0.0.1:8765/
```

## Suggested Next Improvements

- Add a sound on/off toggle, especially for classroom use.
- Add a timed mode or streak milestone display.
- Add a short explanatory/about modal for students.
- Add deterministic seed mode for preparing examples.
- Consider moving the old MATLAB script into a `reference/` folder if the repo should be purely web-app facing.
