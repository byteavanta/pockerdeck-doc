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

-   :material-account-group:{ .lg .middle } **Roles — Admin, Participant, Viewer**

    ---

    Room creator is Admin. Joiners choose Participant or Viewer. Admins can kick, rename, and manage the backlog.

-   :material-format-list-bulleted:{ .lg .middle } **Backlog management**

    ---

    Add stories before creating the room. The Admin picks which item is being voted; completed items are marked Done.

-   :material-docker:{ .lg .middle } **Fully Dockerised**

    ---

    Single-container app. Runs anywhere Docker is available — local or production.

</div>

---

## How it works

1. One team member opens PockerDeck, optionally adds **Backlog Items** and picks an **Estimation Type**, then clicks **+ Create Room** — becoming the **Admin**.
2. Everyone else joins using the **room code** or the shared URL and picks a role (**Participant** or **Viewer**).
3. The Admin selects the first backlog item (or types a story description manually) — it is shared with everyone instantly.
4. Each participant clicks a **card** to cast their vote.
5. Any participant or the Admin clicks **Reveal** — all votes appear at once.
6. The results panel shows the **average**, **minimum**, and **maximum** estimates.
7. Click **New Round** to reset votes and keep estimating, or the Admin picks the next backlog item.
8. Once a story is fully estimated, the Admin clicks **✓ Mark Done** on it in the Backlog panel.

---

## Estimation types

| Type | Default cards |
|------|---------------|
| **Story Points** (default) | `1 2 3 5 8 13 21 34 55 ?` |
| **T-shirt sizes** | `XS S M L XL XXL ?` |
| **Hours** | `3 6 9 12 15 18 21 24 27 30 30+ ?` |
| **Custom** | Any values you define |

Card values can be individually added or removed before creating the room.

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
