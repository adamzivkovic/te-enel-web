# TERMOELEKTRO ENEL AD — Website (homepage preview, repo-ready)

This is a static, framework-free rebuild of the TE ENEL homepage — plain HTML/CSS, no build step, no server required. It's meant to be pushed as-is into a GitHub repo and served with GitHub Pages so it can be shared with colleagues before it goes live on the real domain.

## How to publish it on GitHub Pages

1. Copy everything in this folder (`index.html`, `css/`, `assets/`, `about/`) into the root of your repository (the one you already created) — **replace the existing files entirely**, don't merge by hand.
2. Commit and push:
   ```
   git add .
   git commit -m "Update homepage"
   git push
   ```
3. On GitHub: go to your repo → **Settings → Pages**. Under "Build and deployment", set **Source: Deploy from a branch**, branch **main**, folder **/ (root)**. Save (only needed the first time).
4. GitHub will give you a URL like `https://<your-username>.github.io/<repo-name>/` within a minute or two. That's the shareable preview link — send it to colleagues.
5. **After pushing, hard-refresh your own browser** (Ctrl+Shift+R on Windows/Linux, Cmd+Shift+R on Mac) before checking the result — browsers cache CSS/JS files aggressively, so a normal refresh can keep showing an old stylesheet even after the new one is live on GitHub. If something looks stale or half-updated, this is almost always why.

Because all the paths in `index.html` are **relative** (`assets/img/...`, `css/style.css`, not absolute `/assets/...`), this works correctly whether the repo is served at the root of `username.github.io` or under a subpath like `username.github.io/repo-name/`. No configuration changes needed either way.

## Updating it later

Whenever a new version is ready, just replace `index.html` (and any changed files under `assets/` or `css/`) in the repo and push again — GitHub Pages redeploys automatically, usually within a minute. When the real domain (`te-enel.rs`) is ready to point here, that's a DNS change on the domain's side (a `CNAME` record to `<username>.github.io`, plus a `CNAME` file in this repo) — the site code itself doesn't need to change.

## What's in here

- `index.html` — homepage: hero, About (with a real `#about` section, not just a teaser)/Laboratory/References/Downloads/Partners/News, each with a button through to its own full page
- `laboratory.html`, `references.html`, `downloads.html`, `partners.html`, `contact.html` — every item in the main nav now has its own real page instead of scrolling to a section on the homepage
- `css/style.css` — all styling (shared by every page)
- `about/basic-information.html`, `about/management-board.html`, `about/supervisory-board.html` — the three About Us sub-pages, each a full standalone page with the same header/nav/footer, linked from the "About Us" dropdown in the nav (hover on desktop, tap-to-expand on mobile) and from tabs at the top of each page for jumping between the three
- `assets/img/` — logo and photos (hero, about, ISO certificate scan, reference project photos)
- `assets/docs/` — the real PDF documents linked from the page: construction license, ISO 9001 certificate, lab accreditation certificate, the three reference project lists, the 2026 accredited test methods list, the 2026 technical equipment list, and the four 2026 shareholder-assembly documents — these open/download directly when clicked. The Serbian-original ATS scope document (`obim-akreditacije-01-459.pdf`) is also sitting in this folder ready to go, but intentionally not linked from anywhere yet — it's reserved for the Serbian-language build, where it will replace the English test-methods PDF on the "Accredited test methods" links.

## Header

The header is deliberately minimal now: just the logo (bigger than before) and the nav — no "Contact Us" button and no LinkedIn/YouTube icons in the utility bar. Those social links moved to the Contact page itself, as two more rows in the info table (LinkedIn, YouTube), right under Website.

## The one bit of JavaScript on the site

Everything on this site is plain HTML/CSS by design, with a single deliberate exception: a small inline script (in the shared page template, so it's on every page) that closes the mobile menu overlay when a nav link is clicked. It's a no-op for ordinary links, since navigating to a new page already resets the menu — it only matters for the "About Us" top-level link and the new "Company Overview"/"What We Do" dropdown items, which jump to anchors on the homepage (`#about`, `#video`, `#services`) rather than loading a new page, so nothing would otherwise tell the mobile menu to close.

## Partner logos

The Partners section now shows real logo artwork for 30 of the ~35 companies on the list, supplied directly by the company in batches and checked one by one for watermarks and correct company identity before publishing. The remaining few (CEGT, Pauwels, plain Siemens, Metso) still show as name-only text pills — Metso specifically because the SVG file referenced for it never actually reached this working session and needs to be resent; the rest simply haven't had a logo supplied yet.

## News

- `news/business-news.html`, `news/shareholder-news.html` — split into two sections (matching the old site), linked from a "News" dropdown in the nav (hover on desktop, tap-to-expand on mobile) and from teaser cards on the homepage.
- Business News is an honest empty state — ready to receive real announcements once supplied.
- Shareholder News has a pure-CSS year switcher (2016–2026, no JavaScript) and the 4 real 2026 shareholder-assembly items are now fully wired up: each headline links to its actual supplied PDF (Supervisory Board notice, absentee voting form, voting proxy, assembly minutes). Older years (2016–2025) currently show "no items on file yet" — send that archive too if you'd like it migrated in.

## Site structure — every nav item is now a real page

Every top-level item in the main menu (Laboratory, References, Downloads, Partners, Contact — About Us and News already worked this way) now opens its own standalone page instead of jumping to a section on the homepage. The homepage keeps short teaser versions of each with a button through to the full page. This also fixes a side effect the old anchor-based design had on mobile (see below): tapping a menu item now always loads a real new page, so the menu closes on its own.

## Mobile navigation

Redesigned: tapping the hamburger now opens a full-screen menu (not a dropdown squeezed under the header), and the hamburger icon itself morphs into a close (✕) button in the same spot, so there's always one obvious way to shut it — no more needing to hunt for how to get back to the page. Just as importantly, because every menu item now leads to a real separate page (see above), tapping any link — including the About Us / News sub-items — loads that page directly and the menu closes automatically; it no longer stays open over the content the way it did when everything lived on one page. Still pure CSS, no JavaScript.

## Not in this preview yet

A Serbian-language version of the site (the original Serbian ATS scope document is already in `assets/docs/`, ready for that build — see above), and a full desktop/mobile QA pass beyond the fixes already made. Also still open: the Contact page's actual contact-form mechanism (it currently has phone/e-mail/map/LinkedIn/YouTube only — a real form needs a form service or serverless function since this is a static site), a simple way to add new reference projects/photos later without touching code, and real photos for Industrial Facilities. The Contact page embeds a Google Maps location using the no-API-key `output=embed` format — it couldn't be visually verified in this working environment (no general internet access here), so worth a quick check once it's live that the map tile actually renders.
