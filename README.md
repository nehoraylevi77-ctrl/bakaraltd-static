# bakaraltd-static

Static mirror of https://www.bakaraltd.co.il, regenerated from the live
WordPress site and deployed to Vercel.

## How it's built

The mirror is produced by `../bakaraltd/scripts/mirror.py` (the bakaraltd WP
source repo). It reads the Yoast sitemaps on the live site, downloads every
page + linked CSS/JS/font/image, rewrites absolute URLs to root-relative, and
writes the result here.

## To regenerate

```bash
cd ../bakaraltd
python scripts/mirror.py
```

Then commit and push this repo — Vercel auto-deploys.

## To preview locally

```bash
cd bakaraltd-static
python -m http.server 8765
# open http://localhost:8765/
```

## To deploy to Vercel

```bash
vercel login          # one-time, if the cached token expired
vercel --prod
```

## Known gaps

- Contact forms post to `/wp-admin/admin-ajax.php` which does not exist on
  Vercel. Replace with Formspree / Web3Forms / a Vercel serverless function.
- WP search (`/?s=...`) won't work on a static host. Add Pagefind if needed.
- Logged-in / admin features are gone by design — editing stays on the
  cPanel host.
