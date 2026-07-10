# Q Panel — Cloudflare Workers Proxy Panel

A VLESS over WebSocket proxy panel for Cloudflare Workers. Forked from ZEUS Panel, cleaned and rebranded.

## Deploy

### Option 1: Web Deployer (Easy)

1. Go to the deployer URL
2. Generate a Cloudflare API token with Workers + D1 permissions
3. Paste the token → click deploy
4. Done

### Option 2: Wrangler CLI

```toml
# wrangler.toml
name = "q-panel"
main = "q.js"
compatibility_date = "2024-02-08"

[[d1_databases]]
binding = "DB"
database_name = "q-db"
database_id = "<your-db-id>"

[placement]
mode = "smart"
```

```bash
npx wrangler d1 create q-db
npx wrangler secret put CF_API_TOKEN
npx wrangler secret put CF_ACCOUNT_ID
npx wrangler deploy
```

## After Deploy

- Visit `https://your-worker.workers.dev/panel` to set an admin password
- Add users, configure proxy IP, get VLESS subscription links
- Each user gets a unique UUID-based config

## What's inside

| File | Purpose |
|---|---|
| `q.js` | Main worker — proxy handler + admin panel |
| `ips.txt` | Clean Cloudflare IPs |
| `proxy/` | Proxy lists per country |
| `q deployer.js` | Auto-deployer worker |
