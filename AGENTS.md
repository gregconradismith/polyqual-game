# Agent Instructions

This repository is a static GitHub Pages / PWA version of the original
`polyqualgame.m` idea:

https://gregconradismith.github.io/polyqual-game/

The app teaches qualitative comparison of polynomial curves. Preserve the core
behavior: generate two related polynomial curves, ask whether they are
qualitatively similar, optionally compare signs of `f`, `f'`, and `f''`, then
show a clear reveal/answer-key view with scoring feedback.

Important files:

- `index.html` is the app shell and includes PWA/iPhone metadata.
- `styles.css` contains responsive styling.
- `app.js` contains polynomial generation, qualitative comparison, scoring,
  canvas drawing, answer flow, and sound effects.
- `manifest.webmanifest` defines installable app metadata.
- `service-worker.js` caches the app shell for offline/PWA behavior.
- `icons/` contains app icons.
- `polyqualgame.m` is the original MATLAB reference.
- `CODEX-HANDOFF.md` is the current handoff; `HANDOFF.md` is older historical
  context.

Keep the app dependency-free unless Greg explicitly asks otherwise. Use relative
paths so it works from the project Pages URL.

When changing any app-shell file cached by the service worker, update the cache
name in `service-worker.js` (for example, `polyqual-game-v4`) so browsers and
iPhone Home Screen installs receive the new version.

For JavaScript or service-worker changes, run:

```bash
node --check app.js
node --check service-worker.js
git diff --check
```

For UI, canvas, scoring, sound, or interaction changes, preview locally:

```bash
python3 -m http.server 8765
```

Then open `http://127.0.0.1:8765/` and verify answer flow, reveal state,
score/streak updates, sound-toggle behavior, canvas rendering, and desktop plus
mobile-width layout.

Do not commit local noise such as `.DS_Store`, editor files, or generated
temporary artifacts.
