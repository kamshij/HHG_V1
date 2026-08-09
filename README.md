# HH Goa 2026 — Builder Credential Generator

A single-page, no-build, no-backend app. Upload a photo, fill in your details,
and generate a shareable HH Goa 2026 builder credential (or a square profile
frame), entirely in the browser. Every share post has `#FrameInGoa` locked in.

Visual system is tuned to the HH Goa brand — deep jungle green, bold gold
serif type, and a hot-pink sticker accent — as the default "Jungle" theme,
with Ocean, Tropical, and Cyber as alternate looks.

## What's in here
- `index.html` — the entire app (markup, styles, and logic in one file)
- `manifest.json` + `icon.svg` — makes it installable as a PWA
- `sw.js` — minimal offline service worker

No build step, no `npm install`, no bundler. It's static, plain HTML/CSS/JS.
`heic2any` (for iPhone HEIC photos) loads from a CDN at runtime; the `qrcode`
library is vendored directly inside `index.html`, so QR generation keeps
working even if the page is opened offline or the CDN is unreachable.

## Go live in under a minute

**Option A — GitHub Pages (auto-deploy, included)**
This folder is already a git repo, wired with a GitHub Actions workflow
(`.github/workflows/deploy.yml`) that deploys to Pages on every push to `main`.
1. Create a new **empty** repo on GitHub (no README/license — this folder
   already has one), e.g. `hh-goa-2026`
2. From inside this folder:
   ```
   git remote add origin https://github.com/<you>/<repo>.git
   git branch -M main
   git push -u origin main
   ```
3. In the repo on GitHub: **Settings → Pages → Build and deployment → Source →
   GitHub Actions**. The included workflow will pick it up automatically on
   the push (or re-run it from the **Actions** tab).
4. Your site goes live at `https://<you>.github.io/<repo>/`

**Option B — Vercel / Netlify (drag & drop)**
1. Go to vercel.com/new or app.netlify.com/drop
2. Drag this whole folder in
3. Done — you get a live HTTPS URL immediately

**Option C — Any static host**
Upload the files (`index.html`, `manifest.json`, `icon.svg`, `sw.js`) to
any static file host (S3 + CloudFront, Cloudflare Pages, Firebase Hosting,
your own nginx box). No server-side code is required.

## Notes
- Photos never leave the browser — there's no upload endpoint.
- The "Share on X" button uses Twitter's public Web Intent URL, so it needs no
  API keys or developer account.
- If you rename or move the folder, keep all four files together in the same
  directory (the manifest and service worker use relative paths).
