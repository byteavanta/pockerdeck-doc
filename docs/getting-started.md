# Quick Start

Get PockerDeck running in under two minutes.

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) **22+** (or Docker Desktop)
- Docker Compose **v2** (included with Docker Desktop and newer Docker Engine installs)

---

## Option A — Docker Compose (recommended)

### 1. Clone the repository

```bash
git clone https://github.com/byteavanta/pockerdeck.git
cd pockerdeck
```

### 2. Start the app

```bash
docker compose up -d --build
```

### 3. Open the app

Open [http://localhost:8000](http://localhost:8000) in your browser.

!!! tip
    The `-d` flag runs the container in the background. Remove it if you want to see live logs.

---

## Option B — Pre-built image from Docker Hub

If you just want to run it without cloning the source:

```bash
docker run -d -p 8000:8000 --restart unless-stopped ceco556/pockerdeck:latest
```

Visit [http://localhost:8000](http://localhost:8000).

---

## Option C — Python (no Docker)

Suitable for local development or testing without Docker.

### 1. Clone and enter the repo

```bash
git clone https://github.com/byteavanta/pockerdeck.git
cd pockerdeck
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Run the dev server

```bash
cd app
uvicorn main:app --reload
```

The app is available at [http://localhost:8000](http://localhost:8000).

!!! warning
    The `--reload` flag is for development only. Do not use it in production.

---

## Verify everything is running

After starting the app, create your first room:

1. Open [http://localhost:8000](http://localhost:8000).
2. Click **+ Create Room**.
3. Enter your display name and you're ready to go.

---

## Next steps

- [Usage Guide](usage.md) — full walkthrough of all features
- [Configuration](configuration.md) — adjust the port and other settings
- [Deployment](deployment.md) — deploy to a server
