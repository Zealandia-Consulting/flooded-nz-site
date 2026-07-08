# flooded-nz-site

The "Your Flood Experiences" page — a single static HTML page that embeds an Esri ArcGIS Survey123 form full-viewport in an iframe, for collecting public flood photos/videos to help make communities more resilient to future flooding.

Live at [flooded.nz](https://flooded.nz). `flooded.co.nz` redirects to it at the domain registrar level.

## Hosting

Hosted on **GitHub Pages**, deployed automatically on every push to `main` via [.github/workflows/pages.yml](.github/workflows/pages.yml) — no manual deploy step, no separate cloud account.

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

## Hosting decision

A few hosting options were considered for this page before settling on GitHub Pages:

- **GitHub Pages (chosen)** — free, with no separate cloud account to manage; the repo that holds the code is the same place that serves it. Publishing is a plain `git push`. Free custom domain with a free, auto-renewing HTTPS certificate.
- **Azure Static Web Apps** — also free-tier capable, and also supports custom domains with a free managed certificate. But it needs a separate Azure subscription, and publishing needs either a GitHub Actions integration (more moving parts — a deployment token stored as a secret, an automation file wiring the two platforms together) or a manual CLI deploy step run by hand.

For a single static page with no backend and no build step, GitHub Pages needed the least new infrastructure to stand up and the fewest moving parts to keep working over time — nothing to patch, renew, or re-authenticate beyond GitHub itself.

**DNS:** `flooded.nz`'s domain (registered with 1st Domains) points straight at GitHub Pages via four `A` records at the domain's root — no CDN or proxy service sits in between. `flooded.co.nz` is a separate domain that simply forwards to `flooded.nz` at the registrar level, so it didn't need its own hosting setup at all.

**Reliability:** GitHub Pages runs on the same infrastructure GitHub itself uses, so for a low-traffic single page it's no less reliable in practice than any other mainstream static host. The one real tradeoff versus a paid platform is that GitHub Pages has no formal uptime guarantee (it's "best effort" rather than a contractual SLA) — acceptable here given the page's traffic and purpose.
