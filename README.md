## 👋 Welcome to valkey 🚀

Valkey - open source Redis compatible key/value store

## 📋 Description

Valkey - open source Redis compatible key/value store

## 🚀 Services

- **db**: Valkey key/value store - the deployed product
- **admin**: phpRedisAdmin - web management console



## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/valkey/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/valkey" ~/.local/srv/docker/valkey
cd ~/.local/srv/docker/valkey
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install valkey
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
BASE_HOST_NAME=valkey.example.com
APP_ORG_NAME=Valkey
DB_ADMIN_PASS=replace-with-a-random-password
```

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
| `docker-compose.yaml` | Default, published on `172.17.0.1:64381` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Valkey**: `172.17.0.1:6379` (native protocol port)
- **Web Console**: http://172.17.0.1:64381

## 📂 Volumes

- `./volumes/db/valkey/valkey` - Valkey data

## 🔐 Security

- Set a strong `DB_ADMIN_PASS` - it is the Valkey `requirepass` value
- Port 6379 is published on the host in the default compose file so other stacks can reach Valkey; the proxy variants publish no ports at all
- Back up `./volumes/db/valkey/valkey` regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f admin
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
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
