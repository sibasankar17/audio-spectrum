# Stem Sorter

A fully client-side audio library analyzer & player. Drop in audio files or a whole folder
(scanned recursively), and it decodes and analyzes each track **in your browser** — frequency
zones, musical key, tempo, texture, dynamics — then sorts them into multiple buckets, with a
live spectrum/spectrogram player, multi-band EQ, hot cues, playlist export, and persistent
storage. Nothing is uploaded; all processing is local.

## Deploy to GitHub Pages

The whole app is a single `index.html` (plus an empty `.nojekyll`). No build step, no server.

### Option A — GitHub website (no command line)
1. Create a new repository (e.g. `stem-sorter`). Public repos get free Pages.
2. Click **Add file → Upload files**, drag in `index.html` and `.nojekyll`, and commit.
3. Go to **Settings → Pages**.
4. Under **Build and deployment**, set **Source: Deploy from a branch**, **Branch: `main` / `/ (root)`**, and **Save**.
5. Wait ~1 minute. Your app is live at:
   `https://<your-username>.github.io/<repo-name>/`

### Option B — Command line (git)
```bash
git init
git add index.html .nojekyll README.md
git commit -m "Stem Sorter"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```
Then enable Pages as in steps 3–5 above.

### Option C — GitHub CLI
```bash
gh repo create <repo-name> --public --source=. --remote=origin --push
gh api -X POST repos/<your-username>/<repo-name>/pages -f source.branch=main -f source.path=/
```

## Why hosting helps
- **Secure origin (https):** IndexedDB and localStorage are reliable (some browsers restrict them on `file://`).
- **Web Workers:** the parallel analysis workers (created from a Blob) run without the `file://` restrictions some browsers impose.
- **Shareable:** anyone with the link can use it; their audio still never leaves their machine.

## Notes
- `.nojekyll` tells Pages to serve files as-is (skip Jekyll processing). Keep it in the repo root.
- The app loads two web fonts from Google Fonts over https; everything else is self-contained.
- Folder **drag-and-drop** is Chromium/Safari; the **Scan folder** button works in those plus Firefox.
- Captured playback data, the analysis cache, and your saved library live in the browser's
  IndexedDB/localStorage for that origin — they persist across visits and are private to each user.
