# flooded-nz-site

The deployable "Your Flood Experiences" page — a single static HTML page that embeds an Esri ArcGIS Survey123 form full-viewport in an iframe, for collecting public flood photos/videos.

Served at [flooded.nz](https://flooded.nz) via GitHub Pages (`flooded.co.nz` redirects to it at the registrar level).

## Layout

```
site/                          the actual deployable page
├── index.html                 GTM tag + Open Graph tags + the Survey123 iframe
├── index.html.certlyfe        leftover test file from earlier setup, harmless, left in place
├── CNAME                      GitHub Pages custom domain (flooded.nz)
├── media/                     images used by the Open Graph tags
└── staticwebapp.config.json   CSP/security headers, only relevant if this ever moves to Azure Static Web Apps
.github/workflows/pages.yml     deploys site/ to GitHub Pages on every push to main
```

`site/` (this repo's subfolder) is the actual page — kept separate from this repo's root so this readme and any other light documentation can live here without becoming part of the published page.

## Deploying

Push to `main`. The `pages.yml` workflow uploads `site/` as the Pages artifact and deploys it automatically — no manual steps.

## Parent project

This repo is a submodule of a private planning repo that holds the AWS/Azure/GitHub Pages migration plans, deploy scripts for other hosting targets, and internal notes. This repo only holds what's actually published.
