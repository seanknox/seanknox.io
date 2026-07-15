# seanknox.io

Static rebuild of seanknox.io. Hand-written semantic HTML, one stylesheet, self-hosted
images. No framework, no build step, no backend.

```
index.html          Home
services.html       Services
about.html          About
assets/css/style.css
assets/img/         Self-hosted images
```

## Local preview

```sh
python3 -m http.server 8000
# http://localhost:8000
```

Or just open `index.html` — all paths are relative.

## Images

Only two originals were recoverable from the old Squarespace CDN. Both were served as
WebP under `.png` / `.jpg` extensions and have been saved with their true extension:

| File | Source | Notes |
|---|---|---|
| `assets/img/sean-headshot.webp` | `Sean+Headshot.png` | 824×1003, actually WebP |
| `assets/img/studio-portrait.webp` | `20140301_Trade-151_0124-copy.jpg` | 2200×1400, actually WebP |

These 404 on the CDN and are **not** substituted with stock — a marked placeholder slot
sits in `about.html` instead:

- `20140302_Trade+151_0503.jpg` (home hero on old site)
- `20140228_Trade+151_0067+(1).jpg`
- `landing-full-topleft-01.jpg` (about hero on old site)

Owner to supply originals.

## Deliberately omitted

Squarespace boilerplate: the `/cart` link and the LinkedIn href pointing at
`linkedin.com/company/squarespace`.

## Follow-ups (not done)

- **Hosting:** GitHub Pages, deploy from repo root. Add a `CNAME` file at deploy time.
- **DNS (Namecheap):** apex `seanknox.io` → A records `185.199.108.153`, `185.199.109.153`,
  `185.199.110.153`, `185.199.111.153`; `www` → CNAME `SeanKnox.github.io`. Enforce HTTPS
  after the cert issues.
- **Open decision:** canonical is currently `www.seanknox.io`. Confirm apex vs www, redirect
  the other, then set canonical tags. No canonical tags are set yet, pending this.
- **Contact:** real LinkedIn / contact URLs to be wired into the footer (`TODO` comment in
  each page).

## Remote

Intended: `github.com/SeanKnox/seanknox.io`. Not configured or pushed yet.
