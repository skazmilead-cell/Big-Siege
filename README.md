# Bug Siege — PWA Package

This folder turns your game into an installable Progressive Web App (PWA) —
the format PWABuilder needs in order to generate an Android `.apk`/`.aab`.

## What's inside
- `index.html` — your game, with PWA hooks added (manifest link + service worker)
- `manifest.json` — tells Android/Chrome the app's name, colors, and icons
- `sw.js` — service worker; caches the game so it still loads and plays with no connection
- `icons/` — app icons already generated at the sizes Android needs (192px, 512px, and a padded "maskable" version for adaptive icon shapes)

Nothing about the game itself changed — it plays exactly the same. These files just make it installable.

## Step 1 — Host it somewhere public
PWABuilder needs a live URL to inspect, so pick one (both are free, no server needed):

**Netlify Drop (fastest, no account)**
1. Go to `app.netlify.com/drop`
2. Drag this whole folder onto the page
3. You get a live URL immediately

**GitHub Pages**
1. Create a new repo and upload everything in this folder, keeping the `icons/` subfolder intact
2. Repo → Settings → Pages → set source to your main branch
3. Your site is live at `https://yourusername.github.io/reponame/`

Either way, keep the folder structure exactly as-is (`icons/` must stay a subfolder next to `index.html`).

## Step 2 — Confirm it actually installed correctly
Open your hosted link in Chrome. You should see an install icon in the address bar
(desktop) or an "Add to Home screen" / "Install app" prompt (Android). If that shows
up, the manifest and service worker are wired up correctly.

## Step 3 — Generate the Android package
1. Go to `pwabuilder.com`
2. Paste your hosted URL → Start
3. Open the **Android** card → Generate Package
4. Choose **"Generate a signed package"** — this gives you a real signing key.
   **Save that key somewhere safe** — you'll need the exact same one for every future update.
5. Download the zip. Inside you'll find:
   - a `.apk` — install this directly on your own phone to test
   - a `.aab` — this is the file you upload to Google Play

## Step 4 (optional) — Remove the browser address bar
By default the Android app may show a thin browser bar the first time. To make it
fully full-screen, PWABuilder will give you a fingerprint to put in a file called
`assetlinks.json`. Upload that file to:
```
https://yourdomain.com/.well-known/assetlinks.json
```
on the same hosting from Step 1. This proves you own the site, and the address bar disappears.

## Want a different icon?
Swap the three PNGs in `icons/` for your own art, keeping the same filenames and pixel
sizes (192×192 and 512×512 twice). The current ones are a simple pine-green-and-ladybug
icon matching the game's look.
