# Toy Chest Arcade

A toddler-friendly browser arcade — self-contained, works offline, installable as an app.

## Structure
```
index.html              the whole arcade (all 3 games are inline, no external deps)
manifest.json           PWA metadata (name, icons, standalone display)
service-worker.js       caches everything for offline play
icons/
  icon-192.png
  icon-512.png
  icon-maskable-512.png
.well-known/
  assetlinks.json       placeholder — fill in real values after packaging with PWABuilder
```

## Hosting
Enable GitHub Pages: repo **Settings → Pages → Source → Deploy from branch → main → / (root)**.
Site will be live at `https://<username>.github.io/<repo-name>/`.

## Turning it into an installed Fire tablet app
1. Confirm the Pages URL loads and the service worker registers (DevTools → Application tab).
2. Run the URL through pwabuilder.com → Package for Stores → Android → **signed** package.
3. Copy the SHA-256 fingerprint PWABuilder gives you, and your chosen package name
   (e.g. `com.yourname.toychestarcade`). Replace the placeholders in
   `.well-known/assetlinks.json` with those two values and push.
   - Note: GitHub's drag-and-drop upload sometimes hides dot-folders. If it doesn't
     appear, use "Add file → Create new file" and type the full path
     `.well-known/assetlinks.json` into the filename box — GitHub creates the folder automatically.
4. Sideload the `.apk` PWABuilder generated onto the tablet (enable "Apps from Unknown
   Sources" first).

## Updating the game later
Edit `index.html`, then bump `CACHE_NAME` in `service-worker.js` (e.g. `v2`) so the
tablet fetches the new version instead of serving the old cached one forever.
