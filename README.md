# Skyline 45 site

Plain HTML/CSS/JS. No build step, no framework, no dependencies. Loads fast on purpose.

## Fill in content

Edit `index.html` — every `[bracketed placeholder]` is something to replace:
- Hero tagline, about bio, CV entries, references, contact info.
- Video captions and Vimeo IDs (`data-vimeo-id="..."` — the number in a vimeo.com/123456789 URL).

## Add photos

Drop files into `images/`:
- `portrait.jpg` — headshot for the About section.
- `photo1.jpg` ... `photo6.jpg` — portfolio grid (add more `<figure>` blocks in the `.grid` if you have more than 6).
- `video1-thumb.jpg`, `video2-thumb.jpg` — thumbnail frame for each video facade (grab a frame from Vimeo or a screenshot).

Keep photos web-sized (long edge ~2000px, JPEG quality ~80) so the site stays fast — full 40MB camera RAWs will make it slow. `sips` (built into macOS) can batch-resize:

```bash
cd images
for f in *.jpg; do sips -Z 2000 "$f"; done
```

## Optional: CV PDF

Drop a `cv.pdf` in this folder — the "Download full CV" link already points at it.

## Deploy to Cloudflare Pages

One-time setup:
```bash
cd ~/Scripts/skyline45-site
npx wrangler login
```
This opens a browser to authorize wrangler with your Cloudflare account (the domain is already on Cloudflare, so this uses the same login).

Deploy:
```bash
npx wrangler pages deploy . --project-name=skyline45
```
First run creates the Pages project and gives you a `skyline45.pages.dev` URL. Re-run the same command any time you want to push changes.

## Point your domain at it

In the Cloudflare dashboard: Workers & Pages → skyline45 → Custom domains → add your domain (e.g. `skyline45.com` or `www.skyline45.com`). Cloudflare handles the DNS + SSL automatically since the domain's already in your account.
