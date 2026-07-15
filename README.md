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

These 404 on the old CDN and were **not** substituted with stock:

- `20140302_Trade+151_0503.jpg` (home hero on old site)
- `20140228_Trade+151_0067+(1).jpg`
- `landing-full-topleft-01.jpg` (about hero on old site)

The pages simply run without them. If the originals turn up, the home hero is the
obvious place for the first one.

## Deliberately omitted

Squarespace boilerplate: the `/cart` link and the LinkedIn href pointing at
`linkedin.com/company/squarespace`.

## Deploy

Hosted on GitHub Pages, served from the repo root of `main`.

Canonical host is the **apex**, `https://seanknox.io`. `CNAME` contains `seanknox.io`,
and every page carries a matching `<link rel="canonical">`. GitHub Pages redirects
`www` → apex automatically once the `www` CNAME record below is in place.

### Order of operations

Add the custom domain in **Settings → Pages** *before* pointing DNS at GitHub. Doing it
the other way round leaves a window where another GitHub user could claim `seanknox.io`
on their own repo. Optionally verify the domain first (Settings → Pages → custom domain
verification), which locks the domain to this account permanently.

### DNS (Namecheap)

Delete Squarespace's existing `@` and `www` records first. Namecheap won't save an ALIAS
on a host that still has a conflicting A/AAAA/CNAME/URL-redirect record, and leftover
records on `@` can also stop the GitHub HTTPS cert from issuing.

**Preferred — ALIAS at the apex.** Namecheap supports ALIAS on BasicDNS.

| Host | Type | Value |
|---|---|---|
| `@` | ALIAS | `SeanKnox.github.io.` |
| `www` | CNAME | `SeanKnox.github.io.` |

An ALIAS resolves to whatever IPs GitHub is currently using, so it survives GitHub
renumbering. Prefer it.

**Fallback — A records**, if ALIAS is unavailable for any reason. Use these *instead of*
the ALIAS, never alongside it:

| Host | Type | Value |
|---|---|---|
| `@` | A | `185.199.108.153` |
| `@` | A | `185.199.109.153` |
| `@` | A | `185.199.110.153` |
| `@` | A | `185.199.111.153` |
| `www` | CNAME | `SeanKnox.github.io.` |

Optional IPv6, only with the A-record route (GitHub advises keeping the A records too,
given uneven IPv6 adoption): AAAA on `@` → `2606:50c0:8000::153`, `2606:50c0:8001::153`,
`2606:50c0:8002::153`, `2606:50c0:8003::153`.

The `www` CNAME is worth having either way — GitHub recommends it alongside an apex for
HTTPS, and it's what makes Pages auto-redirect `www` → apex.

Then wait for the cert to issue (up to 24h, usually far less) and tick **Enforce HTTPS**.

Verify with:

```sh
dig seanknox.io +noall +answer
dig www.seanknox.io +noall +answer
```

## Follow-ups

- **Contact:** real LinkedIn / contact URLs to be wired into the footer (`TODO` comment
  in each page).
- **Images:** three originals still missing (see above).
