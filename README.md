# Shiori

A self-hosted application for managing shiori.

## Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/shiori/main/docker-compose.yaml" | docker compose -f - up -d
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

## Configuration

See docker-compose.yaml for environment variables and configuration options.

## Documentation

Check the official project documentation for detailed setup and usage information.
