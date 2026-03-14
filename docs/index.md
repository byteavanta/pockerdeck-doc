# PockerDeck

**PockerDeck** is a lightweight, real-time **Planning Poker** app for agile teams.  
No account, no sign-up — create a room, share the link, and start estimating immediately.

<div class="grid cards" markdown>

-   :material-lightning-bolt:{ .lg .middle } **Instant rooms**

    ---

    Spin up a voting session in one click. Share the 8-character code or URL with your team.

-   :material-wifi:{ .lg .middle } **Real-time WebSockets**

    ---

    Every vote and reveal is pushed to all participants instantly — no polling, no refreshes.

-   :material-eye-off:{ .lg .middle } **Private until revealed**

    ---

    Votes stay hidden until the host clicks **Reveal**. Prevents anchoring bias.

-   :material-docker:{ .lg .middle } **Fully Dockerised**

    ---

    Single-container app. Runs anywhere Docker is available — local or production.

</div>

---

## How it works

1. One team member opens PockerDeck and creates a **room**.
2. Everyone else joins using the **room code** or the shared URL.
3. Each participant enters their **display name** and picks a **story point card**.
4. The host clicks **Reveal** — all votes appear at once.
5. The results panel shows the **average**, **minimum**, and **maximum** estimates.
6. Click **New Round** to reset and move on to the next story.

---

## Card values

| Card | Points |
|------|--------|
| `3`  | 3 |
| `6`  | 6 |
| `9`  | 9 |
| `12` | 12 |
| `15` | 15 |
| `18` | 18 |
| `21` | 21 |
| `24` | 24 |
| `27` | 27 |
| `30` | 30 |
| `30+` | More than 30 (needs splitting) |
| `?`  | Unsure / need more info |

---

## Tech stack

| Layer | Technology |
|-------|-----------|
| Backend | [FastAPI](https://fastapi.tiangolo.com/) |
| Real-time | WebSockets (native FastAPI support) |
| Frontend | Vanilla HTML / CSS / JavaScript |
| Templating | Jinja2 |
| Container | Docker + Docker Compose |

---

## Quick start

```bash
docker run -p 8000:8000 ceco556/pockerdeck:latest
```

Open [http://localhost:8000](http://localhost:8000) and you're good to go.

[Get started :material-arrow-right:](getting-started.md){ .md-button .md-button--primary }
[View on GitHub :material-github:](https://github.com/byteavanta/pockerdeck-doc){ .md-button }
