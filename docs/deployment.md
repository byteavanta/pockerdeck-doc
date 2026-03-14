# Docker Deployment

This page covers deploying PockerDeck to a production server using Docker.

---

## Minimal `docker-compose.yml`

The simplest production configuration:

```yaml title="docker-compose.yml"
services:
  web:
    image: ceco556/pockerdeck:latest
    ports:
      - "8000:8000"
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "python", "-c", "import urllib.request; urllib.request.urlopen('http://localhost:8000/')"]
      interval: 30s
      timeout: 5s
      retries: 3
      start_period: 10s
```

Deploy with:

```bash
docker compose up -d
```

---

## Updating to a newer image

```bash
docker compose pull
docker compose up -d
```

---

## Persisting rooms across restarts

!!! warning "In-memory storage"
    PockerDeck currently stores all room data **in memory**. Rooms are lost when the container restarts. This is intentional for simplicity — planning poker sessions are ephemeral by nature.

    A future release may add optional persistence. For now, teams should simply create a new room after a restart.

---

## Resource requirements

PockerDeck is extremely lightweight:

| Resource | Typical usage |
|----------|--------------|
| RAM | ~50 MB |
| CPU | Negligible (idle) |
| Disk | ~200 MB (image) |

It runs comfortably on the smallest cloud VMs (1 vCPU / 512 MB RAM).
