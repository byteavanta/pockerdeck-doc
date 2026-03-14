# Docker Hub

PockerDeck is published as a public image on Docker Hub.

**Image:** [`ceco556/pockerdeck`](https://hub.docker.com/r/ceco556/pockerdeck)

---

## Pulling the image

```bash
docker pull ceco556/pockerdeck:latest
```

---

## Running from Docker Hub

```bash
docker run -d \
  --name pockerdeck \
  -p 8000:8000 \
  --restart unless-stopped \
  ceco556/pockerdeck:latest
```

---

## Available tags

| Tag | Description |
|-----|-------------|
| `latest` | Most recent stable build |

---

## Image details

| Property | Value |
|----------|-------|
| Base image | `python:3.12-slim` |
| Exposed port | `8000` |
| Working directory | `/app` |
| Entrypoint | `uvicorn main:app --host 0.0.0.0 --port 8000` |
