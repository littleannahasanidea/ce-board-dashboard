# CE Board Exam Dashboard — PWA

Everything in this folder is what you deploy. Keep the folder structure
exactly as-is (the `icons/` folder has to stay next to `index.html`,
`manifest.json`, and `sw.js` — the paths inside those files depend on it).

## Deploy to GitHub Pages (free)

1. Go to github.com and create a new repository (e.g. `ce-board-dashboard`).
   Public repos get free Pages hosting.
2. Upload every file in this folder into the repo, preserving the
   `icons/` subfolder. Easiest way: on the repo page, click
   **Add file → Upload files**, drag in `index.html`, `manifest.json`,
   `sw.js`, `README.md`, and the whole `icons` folder, then commit.
3. Go to the repo's **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a
   branch**. Under **Branch**, choose `main` and folder `/ (root)`,
   then **Save**.
5. GitHub gives you a URL like:
   `https://<your-username>.github.io/ce-board-dashboard/`
   It can take a minute or two to go live the first time.
6. Open that link on your phone/tablet browser, then use the browser's
   **"Add to Home Screen"** / **install** option (Chrome shows an
   install icon in the address bar; Safari on iOS uses the Share sheet
   → Add to Home Screen). It'll behave like a real installed app —
   own icon, own window, no browser bar.

## Offline behavior

The service worker (`sw.js`) caches the app shell the first time you
open it online. After that, opening the app with no connection will
still load it from cache. Any data you enter (schedule, quiz banks,
exam keys, personal log photos, etc.) is stored locally in the
browser via `localStorage` — nothing is sent anywhere, and nothing
needs a connection to work.

**One caveat:** the two Google Fonts (Manrope, Sora) load from
Google's CDN and are not cached by the service worker. Offline, the
app will still fully work — it'll just fall back to your device's
default system font instead of those two.

## Updating the app later

Whenever you upload a new version of `index.html` (or anything else),
bump the `CACHE_NAME` value at the top of `sw.js` (e.g. `v1` → `v2`).
That tells every installed copy to drop its old cache and fetch the
new files next time it's opened online. If you forget to bump it,
people may keep seeing the old cached version for a while.

## Files in this folder

- `index.html` — the whole app (single file, all CSS/JS inline)
- `manifest.json` — tells the browser/OS this is an installable app,
  its name, colors, and icons
- `sw.js` — the service worker that makes offline mode work
- `icons/` — all generated app icons (see below)

## About the icons

Generated to match the app's navy/purple/orange palette:
- `icon-192.png`, `icon-512.png` — standard app icons (rounded)
- `icon-maskable-512.png` — "maskable" version with extra padding so
  Android can safely crop it into a circle/squircle without cutting
  off the logo
- `apple-touch-icon.png` — used by iOS when added to the home screen
- `favicon.ico`, `favicon-16.png`, `favicon-32.png` — browser tab icon

If you ever want a different icon design, just ask and I can
regenerate this whole set.
