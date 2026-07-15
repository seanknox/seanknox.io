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
| `assets/img/sean-headshot.webp` | `Sean+Headshot.png` | 824×1003, actually WebP. Photo of Sean. |
| `assets/img/landscape-lake-mountains.webp` | `20140301_Trade-151_0124-copy.jpg` | 2200×1400, actually WebP. **Despite the Trade 151 filename this is landscape scenery, not a portrait and not a photo of Sean.** Used as decorative home hero (empty `alt`) pending the real hero image. |

These 404 on the CDN and are **not** substituted with stock — a marked placeholder slot
sits in `about.html` instead:

- `20140302_Trade+151_0503.jpg` (home hero on old site)
- `20140228_Trade+151_0067+(1).jpg`
- `landing-full-topleft-01.jpg` (about hero on old site)

Owner to supply originals.

## Deliberately omitted

Squarespace boilerplate: the `/cart` link and the LinkedIn href pointing at
`linkedin.com/company/squarespace`.

## Deploy

Hosted on GitHub Pages, served from the repo root of `main`.

Canonical host is the **apex**, `https://seanknox.io`. `CNAME` contains `seanknox.io`,
and every page carries a matching `<link rel="canonical">`. GitHub Pages redirects
`www` → apex automatically once the `www` CNAME record below is in place.

### DNS (Namecheap)

| Host | Type | Value |
|---|---|---|
| `@` | A | `185.199.108.153` |
| `@` | A | `185.199.109.153` |
| `@` | A | `185.199.110.153` |
| `@` | A | `185.199.111.153` |
| `www` | CNAME | `SeanKnox.github.io.` |

Remove Squarespace's existing records for `@` and `www` first, or they'll conflict.
Then in the repo: Settings → Pages → set the custom domain to `seanknox.io`, wait for
the cert to issue, and tick **Enforce HTTPS**.

## Follow-ups

- **Contact:** real LinkedIn / contact URLs to be wired into the footer (`TODO` comment
  in each page).
- **Images:** three originals still missing (see above).
