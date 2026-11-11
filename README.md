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

The site is live on GitHub Pages:

- `.github/workflows/pages.yml` deploys the `public` folder on every push to `main`.
- GitHub Pages is enabled with **Source: GitHub Actions**.
- Live site: `https://peakeggfinder.github.io/peakeggfinder/`
- All page links are relative, so the project URL works correctly.

After editing, deploy with:

```cmd
cd /d "C:\Users\Fiz\Documents\Default Project\egg-dashboard-netlify"
git add .
git commit -m "Update dashboard"
git push
```

There is no build step and no deploy credit limit.

## Separate logs per client

In `/admin`, create a client token and either leave **Egg Log Bot ID** blank
(auto-generated) or enter your own `bot_...` ID. Copy both the token and bot ID
to the client.

In the Lua bot:

```lua
EGGLOG_BOT_ID = "bot_xxxxxxxxxxxxxxxx"
```

The bot adds that ID to each Cloudflare POST. Client tokens are filtered by
their assigned bot ID, so each client sees only their own pet logs. Admin sees
all logs. If `EGGLOG_BOT_ID` is blank, logs remain unassigned/shared.

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
