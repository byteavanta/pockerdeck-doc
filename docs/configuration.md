# Configuration

PockerDeck is intentionally zero-config for most use cases — sensible defaults are baked in. The only common setting you may want to change is the **port**.

---

## Changing the port

=== "Docker Compose"

    Edit `docker-compose.yml` and change the host-side port number (left of the colon):

    ```yaml title="docker-compose.yml" hl_lines="4"
    services:
      web:
        image: ceco556/pockerdeck:latest
        ports:
          - "9000:8000"  # (1)
    ```

    1. The container always listens on `8000` internally. Only the left-hand side needs changing.

    Then restart:

    ```bash
    docker compose up -d
    ```

=== "docker run"

    Pass a different host port with `-p`:

    ```bash
    docker run -d -p 9000:8000 ceco556/pockerdeck:latest
    ```

=== "Uvicorn (no Docker)"

    Pass `--port` to `uvicorn`:

    ```bash
    uvicorn main:app --host 0.0.0.0 --port 9000
    ```

---

## Health check

The official Docker image ships with a built-in health check that polls the `/` endpoint every 30 seconds:

```yaml
healthcheck:
  test: ["CMD", "python", "-c", "import urllib.request; urllib.request.urlopen('http://localhost:8000/')"]
  interval: 30s
  timeout: 5s
  retries: 3
  start_period: 10s
```

This is already included in `docker-compose.yml`. If you use a custom `docker run` command, you can add `--health-cmd` to replicate it.

---

## Environment variables

PockerDeck currently stores all room state **in memory**. No database connection strings or API keys are required. Future versions may expose env vars for persistence options.

---

## Reverse proxy (HTTPS)

When running behind a reverse proxy such as **Nginx** or **Caddy**, make sure WebSocket upgrade headers are forwarded:

=== "Nginx"

    ```nginx
    location / {
        proxy_pass         http://localhost:8000;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection "upgrade";
        proxy_set_header   Host $host;
    }
    ```

=== "Caddy"

    ```caddyfile
    your.domain.com {
        reverse_proxy localhost:8000
    }
    ```

    Caddy handles WebSocket upgrades automatically.

!!! info
    Without proper WebSocket proxying, participants will be unable to connect and will see a "Connection error" badge.
