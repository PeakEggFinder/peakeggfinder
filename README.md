# Egg Finder - static dashboard

Static dashboard, admin panel and bot tracker for the Egg Finder backend.

```
Bots -> Cloudflare API Worker -> D1
                 ^
                 | direct HTTPS API
             GitHub Pages
```

- The browser calls `https://egg-pet-logs.egg-pet-logs.workers.dev/api/*` directly.
- No API proxy and no server-side functions are required.
- Client/admin tokens, expiry, Auto Join settings and Bot Status live in Cloudflare D1.
- Auto Join launches the exact server; full servers stay clickable.

## GitHub Pages deployment

The site is ready for GitHub Pages:

- `.github/workflows/pages.yml` deploys the `public` folder on every push to `main`.
- In GitHub: **Settings > Pages > Build and deployment > Source: GitHub Actions**.
- All page links are relative, so the site works from a project URL such as
  `https://YOUR_USERNAME.github.io/peakeggfinder/`.

Create the repository and push:

```cmd
cd /d "C:\Users\Fiz\Documents\Default Project\egg-dashboard-netlify"
git init
git add .
git commit -m "Egg Finder dashboard"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/peakeggfinder.git
git push -u origin main
```

If the GitHub CLI is logged in:

```cmd
gh repo create peakeggfinder --public --source . --remote origin --push
```

There is no build step and no deploy credit limit.

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
