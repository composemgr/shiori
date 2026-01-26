## 👋 Welcome to shiori 🚀

Simple bookmark manager built with Go

## 📋 Description

Simple bookmark manager built with Go

## 🚀 Services

- **shiori**: ghcr.io/go-shiori/shiori:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/shiori/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/shiori" ~/.local/srv/docker/shiori
cd ~/.local/srv/docker/shiori
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install shiori
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
SERVICE_USER=1000
SERVICE_GROUP=1000
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:8088

## 📂 Volumes

- `./rootfs/config/shiori` - Data storage
- `./rootfs/data/shiori` - Data storage

## 🔍 Logging

```shell
docker compose logs -f shiori
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
