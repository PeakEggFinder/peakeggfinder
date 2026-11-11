# Peak Egg Finder v2 - static dashboard

Static dashboard + admin panel for the Cloudflare Worker + D1 pet-log backend.

```
Bots -> Cloudflare Worker -> D1
                 ^
                 | direct HTTPS API
          Static dashboard
```

- The browser calls `https://egg-pet-logs.egg-pet-logs.workers.dev/api/*` directly.
- No API proxy and no server-side functions are required.
- Client/admin tokens, expiry, Auto Join settings and Bot Status live in Cloudflare D1.
- Auto Join launches the exact server; full servers stay clickable.

## Current deployment (free, no Netlify credits)

Cloudflare Workers static assets:

```cmd
cd /d "C:\Users\Fiz\Documents\Default Project\egg-dashboard-netlify"
npx wrangler deploy
```

Live at:

```text
https://peakeggfinderv2.egg-pet-logs.workers.dev
```

Deploy again after any HTML change. There is no build step and no per-deploy credit limit.

## GitHub Pages

The site is ready for GitHub Pages:

- `.github/workflows/pages.yml` deploys the `public` folder on every push to `main`.
- In GitHub: **Settings > Pages > Build and deployment > Source: GitHub Actions**.
- Create the repository, push this folder, and the workflow publishes the site.

```cmd
git init
git add .
git commit -m "Egg Finder dashboard"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

All page links are relative, so the site also works from a project URL such as
`https://YOUR_USERNAME.github.io/YOUR_REPO/`.

## API URL

If the Cloudflare API Worker changes, update the `API_BASE` constant in:

- `public/index.html`
- `public/admin.html`

```js
const API_BASE = 'https://egg-pet-logs.egg-pet-logs.workers.dev';
```

## Lua

The bot posts directly to Cloudflare:

```lua
PET_LOG_URL = "https://egg-pet-logs.egg-pet-logs.workers.dev/api/pets"
```
