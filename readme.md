# flooded-nz-site

The "Your Flood Experiences" page — a single static HTML page that embeds an Esri ArcGIS Survey123 form full-viewport in an iframe, for collecting public flood photos/videos to help make communities more resilient to future flooding.

Live at [flooded.nz](https://flooded.nz). `flooded.co.nz` redirects to it at the domain registrar level.

## Hosting

Hosted on **GitHub Pages**, deployed automatically on every push to `main` via [.github/workflows/pages.yml](.github/workflows/pages.yml) — no manual deploy step, no separate cloud account.

A few hosting options were considered for this page:

- **GitHub Pages** (chosen) — free, no separate cloud account needed, publishing is just a `git push`, free custom domain with an auto-renewing HTTPS certificate.
- **Azure Static Web Apps** — also free-tier capable and supports custom domains + certs, but needs a separate Azure subscription and either a GitHub Actions integration or a manual CLI deploy step.

For a single static page with no backend, GitHub Pages was the simplest fit — it needed the least new infrastructure and the fewest moving parts to keep working over time.

## Layout

```
site/                          the actual deployable page
├── index.html                 GTM tag + Open Graph tags + the Survey123 iframe
├── index.html.certlyfe        leftover test file from earlier setup, harmless, left in place
├── CNAME                      GitHub Pages custom domain (flooded.nz)
└── media/                     images used by the Open Graph tags
.github/workflows/pages.yml     deploys site/ to GitHub Pages on every push to main
```

`site/` is a subfolder rather than this repo's root so this readme (and any other light documentation) can live here without becoming part of the published page.

## Making a change

Edit the files under `site/`, commit, and push to `main`. GitHub Pages picks it up automatically within a minute or two.
