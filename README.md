# TERMOELEKTRO ENEL AD — Website (homepage preview, repo-ready)

This is a static, framework-free rebuild of the TE ENEL homepage — plain HTML/CSS, no build step, no server required. It's meant to be pushed as-is into a GitHub repo and served with GitHub Pages so it can be shared with colleagues before it goes live on the real domain.

## How to publish it on GitHub Pages

1. Copy everything in this folder (`index.html`, `css/`, `assets/`) into the root of your repository (the one you already created).
2. Commit and push:
   ```
   git add .
   git commit -m "Add homepage preview"
   git push
   ```
3. On GitHub: go to your repo → **Settings → Pages**. Under "Build and deployment", set **Source: Deploy from a branch**, branch **main**, folder **/ (root)**. Save.
4. GitHub will give you a URL like `https://<your-username>.github.io/<repo-name>/` within a minute or two. That's the shareable preview link — send it to colleagues.

Because all the paths in `index.html` are **relative** (`assets/img/...`, `css/style.css`, not absolute `/assets/...`), this works correctly whether the repo is served at the root of `username.github.io` or under a subpath like `username.github.io/repo-name/`. No configuration changes needed either way.

## Updating it later

Whenever a new version is ready, just replace `index.html` (and any changed files under `assets/` or `css/`) in the repo and push again — GitHub Pages redeploys automatically, usually within a minute. When the real domain (`te-enel.rs`) is ready to point here, that's a DNS change on the domain's side (a `CNAME` record to `<username>.github.io`, plus a `CNAME` file in this repo) — the site code itself doesn't need to change.

## What's in here

- `index.html` — homepage markup
- `css/style.css` — all styling
- `assets/img/` — logo and photos (hero, about, ISO certificate scan, reference project photos)
- `assets/docs/` — the real PDF documents linked from the page (construction license, ISO 9001 certificate, lab accreditation certificate, and the three reference project lists) — these open/download directly when clicked

## Known gap: partner logos

The homepage doesn't yet include a Partners section with company logos. The company presentation lists ~35 partner companies (ABB, Siemens, Alstom, Honeywell, General Electric, Schneider, etc.) but only as plain text — no logo image files exist in the source material, and this working environment currently has no path to download images from the web. A separate list of candidate official logo source URLs (mostly Wikimedia Commons / official brand pages) is being prepared — once the actual image files are available (downloaded manually, or supplied by the company), a Partners page/section can be added the same way the reference photos were.

## Not in this preview yet

This is the **homepage only** — a first design direction to sign off on before the rest of the site is built out: standalone pages for Licenses, full References, Partners, News, and Contact, plus a Serbian-language version and a dedicated mobile QA pass beyond the fixes already made. About Us now includes basic company info, Management/Board (Legal Representative, Executive Board, Supervisory Board) and a simplified organization chart; Licenses/certificates and the reference-list PDFs now live in a dedicated Downloads section. Also still open: the contact form mechanism (needs a form service or serverless function since this is a static site), a simple way to add new reference projects/photos later without touching code, and real photos/logos for Industrial Facilities and the Partners page (see `partner-logo-sources.md`).
