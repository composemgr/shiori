## 👋 Welcome to Shiori 🚀

Simple bookmark manager that beautifully bookmarks web pages you want to keep

## 📋 Description

Shiori is a self-hosted bookmark manager. It imports an exported Netscape
bookmarks HTML file, scrapes a short description and screenshot for each entry
and keeps the archive local. It is a single Go binary, so this stack is one
service and no database container.

State lives in a SQLite database and an archive directory under `/data`. Both
are bind mounted, so upgrading the image is just a `pull` and `up -d`.

## 🚀 Services

- **app**: ghcr.io/go-shiori/shiori:latest

No database or cache container is required; Shiori stores its state in SQLite.

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/shiori/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/shiori" ~/.local/srv/docker/shiori
cd ~/.local/srv/docker/shiori
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install shiori
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
APP_ORG_NAME=Shiori
```

The stack sets Shiori's own settings directly in the compose file rather than
exposing them as variables: `SHIORI_DIR` is `/data`, `SHIORI_DATABASE_URL` is
`sqlite:///data/shiori.db` and `SHIORI_HTTP_ADDRESS` is `0.0.0.0:8080`.
Change those lines if you move the data or listen on a different port.

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64342` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

The single `app` service carries the proxy labels and joins the external
network. Neither proxy variant publishes a port.

Shiori has no external URL setting of its own, so no per-variant environment
change is needed. Run Shiori behind a proxy on a hostname that resolves
correctly if you want the fetched page links and screenshots to line up.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64342

Shiori starts unauthenticated. Create the first account in the web UI right
away, since there is no access control before you do.

## 📂 Volumes

- `./volumes/data/shiori` - SQLite database, archived pages, screenshots
  and assets

## 🔐 Security

- Change all default passwords before deploying to production
- Shiori has no authentication on first start; register the admin account in
  the web UI before exposing the stack
- Use HTTPS via one of the reverse proxy variants in production; scraped
  pages and screenshots are served from the same origin as the UI
- The data directory holds a copy of every page you bookmark, treat it as
  sensitive
- Regularly update Docker images for security patches
- Back up the data directory regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart

# Back up the data directory
tar czf shiori-backup.tar.gz volumes/data/shiori
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+
- At least 512 MB of memory

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
