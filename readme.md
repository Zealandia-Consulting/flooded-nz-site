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

This page is one HTML file with no backend and no build step — it doesn't need a full cloud hosting platform, just somewhere to serve a file over HTTPS with a custom domain. A few options were weighed before settling on GitHub Pages.

### Options considered

**GitHub Pages (chosen)** — free, with no separate cloud account to manage; the repo that holds the code is the same place that serves it. Publishing is a plain `git push` — GitHub notices and serves the new version within a minute or two. Free custom domain with a free, auto-renewing HTTPS certificate, both built in.

**Azure Static Web Apps** — also free-tier capable, and also supports custom domains with a free managed certificate. But it needs a separate Azure subscription and account to manage, and publishing needs either:
- a GitHub Actions integration — more moving parts: a deployment token stored as a secret, plus a workflow file wiring GitHub and Azure together, or
- a manual CLI deploy — no GitHub automation, but still requires the Azure account and a token to be created and looked after.

**Azure Blob Storage (static website hosting)** — the closest like-for-like to a plain storage bucket: drag files in through the Azure portal by hand, no command line needed. It's missing the one thing that made the other two options worth considering, though — there's no free custom domain or auto-renewing HTTPS certificate built in. Getting `flooded.nz` pointed at it with a valid certificate means adding **Azure CDN or Front Door** on top — another product, another bill, another thing to configure — which brings back exactly the kind of multi-product setup this move was meant to get away from.

### Why GitHub Pages

For a single static page that rarely changes, GitHub Pages needed the least new infrastructure to stand up and the fewest moving parts to keep working over time — no separate cloud account, no token to store, nothing to patch or re-authenticate beyond GitHub itself. The Azure options are solid products, but they're sized for something bigger: a growing app with a login system, an API, or a team shipping changes every week, where the automation earns its complexity by removing manual publishing steps entirely for people who'll actually feel that benefit day to day.

### DNS

`flooded.nz` (registered with 1st Domains) points straight at GitHub Pages using four `A` records at the domain's root — no CDN or proxy service sits in between. `flooded.co.nz` is a separate domain that simply forwards to `flooded.nz` at the registrar level, so it never needed its own hosting setup at all.

### Reliability

GitHub Pages runs on the same infrastructure GitHub itself uses (which, notably, runs on Azure under the hood) — for a single low-traffic page, none of the options above is meaningfully more likely to go down than another. The one real difference is around formal support rather than actual uptime: Azure Static Web Apps' paid tier comes with a contractual service-level agreement, while GitHub Pages is explicitly "best effort" with no formal SLA. For a page with this little traffic, that distinction is unlikely to matter in practice — but it's the honest answer if uptime guarantees ever come up.
