# ECHOVEIL

Two separate projects, both plain HTML, CSS and JavaScript. There is no build step, no framework and no npm dependencies.

| Folder | What it is |
|---|---|
| `ECHOVEIL-Website/` | The official website: Home, The Game, Cards, Lore (Echoes, Entities, Factions, Locations, Timeline), Gallery, Play, Store/Wishlist. |
| `ECHOVEIL-Game/` | ECHOVEIL The Game: the single-player dark fantasy card-battle game (80 cards, four-quest campaign, deck builder, 22 achievements). |

The website's **Play** page loads the game from `ECHOVEIL-Website/game/index.html`. That `game/` folder is a copy of `ECHOVEIL-Game/`. After you change the game, refresh the copy (see "Keeping the two in sync").

## Quick start (local)

Use a local web server, because browsers restrict some features when pages are opened as `file://`.

```bash
cd ECHOVEIL-Website && python3 -m http.server 8000   # http://localhost:8000
cd ECHOVEIL-Game    && python3 -m http.server 8001   # http://localhost:8001
```

Any static server works (`npx serve`, VS Code Live Server, and so on). Node and npm are not required.

## Uploading to GitHub

**Recommended: two repositories**, one per project. The contents of the folder become the repository root.

1. On github.com choose **New repository** and create `echoveil-website` (and a second one, `echoveil-game`).
2. In each, choose **Add file > Upload files** and drag in the *contents* of the matching folder (not the folder itself). Commit.
   Or with git:
   ```bash
   cd ECHOVEIL-Website
   git init && git add . && git commit -m "ECHOVEIL website"
   git branch -M main
   git remote add origin https://github.com/<you>/echoveil-website.git
   git push -u origin main
   ```
3. Turn on hosting for each: **Settings > Pages > Deploy from a branch > `main` / root**.

If you prefer **one repository** with both folders, GitHub Pages can only serve the root or `/docs`. Either keep both projects there for storage and deploy the website from a separate repo, or serve it with a Pages workflow that publishes `ECHOVEIL-Website/`.

GitHub's web uploader limits a single upload to 100 files. The website has about 200 files, so upload it in two batches or use git/GitHub Desktop.

## Keeping the two in sync

`ECHOVEIL-Website/tools/sync-game.sh` copies `ECHOVEIL-Game/` into `ECHOVEIL-Website/game/`. Run it from the `ECHOVEIL/` folder after editing the game.

## Notes

- **Fonts** (Cinzel, EB Garamond, Inter) are loaded from Google Fonts. They are open-licensed (SIL OFL), but they are not bundled in these ZIPs, so the sites need internet access to show the intended typefaces. Offline, they fall back to Georgia and system fonts.
- **No secrets** are included. The only configuration is `ECHOVEIL-Website/js/config.js`, which holds optional links (wishlist, support, socials) left empty on purpose.
- **Not browser-tested.** The packaging was checked statically (all file references resolve, all scripts parse), but neither project was opened and played in a browser during export. Open both once before publishing.
