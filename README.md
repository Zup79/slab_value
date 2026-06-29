# Slab Value — PWA (GitHub Pages + glistenandbark.com.au)

A self-contained Progressive Web App. Hosted over HTTPS it installs to a phone
home screen and runs offline.

## Files
- index.html              the app ($/m² headline, $/m³ cross-check, grade bands, suggested price)
- manifest.json           install metadata (name, colours, icons)
- sw.js                   service worker — offline caching
- icon-192 / 512 / 512-maskable .png
- CNAME                   your custom domain (glistenandbark.com.au)
- .nojekyll               tells GitHub Pages to serve files as-is (no Jekyll)

------------------------------------------------------------------
## A. Put it on GitHub Pages
1. Create a new repo (public). Name doesn't matter — e.g. `slab-value`.
2. Upload ALL files in this folder to the repo root
   (GitHub → Add file → Upload files → drag them in → Commit).
3. Repo → Settings → Pages.
   - Source: "Deploy from a branch", Branch: `main`, Folder: `/ (root)`. Save.
4. Wait ~1 min. A `https://<your-username>.github.io/<repo>/` URL appears.
   Confirm the app loads there first.

## B. Point glistenandbark.com.au at it
GitHub side:
   - Settings → Pages → "Custom domain" → type `glistenandbark.com.au` → Save.
     (This matches the CNAME file already in the repo.)

DNS side (at your domain registrar's DNS panel) — apex domain needs A records:
   Type A,  Host @ (blank/apex),  Value:
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
   (Optional IPv6 — Type AAAA, Host @):
     2606:50c0:8000::153
     2606:50c0:8001::153
     2606:50c0:8002::153
     2606:50c0:8003::153
   Recommended www redirect — Type CNAME, Host www, Value: <your-username>.github.io

5. DNS can take up to 24h (often minutes). Back in Settings → Pages, once the
   green tick shows, enable "Enforce HTTPS". A PWA MUST be on HTTPS to install.

## C. Install on your phone
Open https://glistenandbark.com.au in Chrome → menu (⋮) → "Install app" /
"Add to Home screen".

------------------------------------------------------------------
## If the tool is only PART of your site (a subfolder)
If glistenandbark.com.au is your main website and you want the tool at, say,
glistenandbark.com.au/slab-value/ :
   - Move CNAME to the REPO ROOT (one CNAME per domain, at the top level).
   - Put index.html + the rest in a `/slab-value/` subfolder.
   - All paths in here are relative, so it just works at any depth.

## Pushing updates
Edit files, re-upload, and bump `VERSION` in sw.js (v1 → v2) so phones fetch
the new version instead of the cached old one.

## Data
Grade bands + saved slabs live in the browser's localStorage on the device.
Clearing site data wipes them. No server, no account.
