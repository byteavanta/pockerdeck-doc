# Architecture

An overview of how PockerDeck is structured internally.

---

## High-level diagram

```
┌─────────────────────────────────────────────────────┐
│                       Browser                        │
│                                                      │
│  HTML page (Jinja2)   room.js   WebSocket client     │
└──────────┬────────────────┬──────────────────────────┘
           │  HTTP GET      │  ws:// or wss://
           ▼                ▼
┌─────────────────────────────────────────────────────┐
│                    FastAPI app                       │
│                                                      │
│  GET /              → index.html                     │
│  POST /create-room  → create room, redirect          │
│  GET  /room/{id}    → room.html                      │
│  WS   /ws/{id}/{name} → ConnectionManager            │
└──────────────────────────┬──────────────────────────┘
                           │
                ┌──────────▼──────────┐
                │   In-memory store    │
                │   rooms: dict        │
                └─────────────────────┘
```

---

## Components

### FastAPI application (`main.py`)

The entire backend lives in a single file. It handles:

| Route | Method | Purpose |
|-------|--------|---------|
| `/` | `GET` | Serve the landing page |
| `/create-room` | `POST` | Generate a new room ID and redirect |
| `/room/{room_id}` | `GET` | Serve the room page |
| `/ws/{room_id}/{user_name}` | `WebSocket` | Real-time communication |

### ConnectionManager

Maintains a mapping of `room_id → { user_name → WebSocket }`. Provides:

- `connect(room_id, user_name, websocket)` — register a new participant
- `disconnect(room_id, user_name)` — remove a participant
- `broadcast(room_id, message)` — fan-out a JSON message to every participant in a room

Dead connections are silently removed during a broadcast.

### State model

Each room is a plain Python dictionary:

```python
{
    "users": {
        "Alice": {"vote": "8", "role": "admin"},
        "Bob":   {"vote": None, "role": "user"},
        "Carol": {"vote": None, "role": "viewer"},
    },
    "revealed": False,
    "story": "As a user I want to…",
    "admin": "Alice",
    "cards": ["1", "2", "3", "5", "8", "13", "21", "34", "55", "?"],
    "backlog": [
        {"title": "User login", "done": True},
        {"title": "Password reset", "done": False},
    ],
    "active_bli": 1,   # index of the currently voted backlog item, or None
}
```

### `build_state(room_id)`

Assembles the JSON payload broadcast to all clients after any state change. Anonymises votes when `revealed` is `False` — clients only see `"voted"` or `null`, never the actual value until the host reveals. Also includes `admin`, `backlog`, `active_bli`, and the user's `role` in every broadcast.

---

## WebSocket message protocol

All messages are JSON objects.

### Server → Client (`state` message)

Sent after every state change (join, vote, reveal, reset, set_story):

```json
{
  "type": "state",
  "users": {
    "Alice": "voted",
    "Bob": null
  },
  "revealed": false,
  "story": "Story description"
}
```

When `revealed` is `true`, actual vote values are sent instead of `"voted"`:

```json
{
  "type": "state",
  "users": {
    "Alice": "8",
    "Bob": "13"
  },
  "revealed": true,
  "story": "Story description"
}
```

### Client → Server (action messages)

| Action | Allowed roles | Payload | Description |
|--------|--------------|---------|-------------|
| `vote` | admin, participant | `{ "action": "vote", "value": "8" }` | Cast or change a vote |
| `reveal` | admin, participant | `{ "action": "reveal" }` | Reveal all votes |
| `reset` | admin, participant | `{ "action": "reset", "story": "…" }` | Start a new round |
| `set_story` | admin, participant | `{ "action": "set_story", "story": "…" }` | Update the story text |
| `select_bli` | admin | `{ "action": "select_bli", "index": 0 }` | Set the active backlog item |
| `mark_bli_done` | admin | `{ "action": "mark_bli_done", "index": 0 }` | Mark a backlog item as done |
| `kick` | admin | `{ "action": "kick", "target": "Bob" }` | Remove a user from the room |
| `rename_user` | admin | `{ "action": "rename_user", "target": "Bob", "new_name": "Robert" }` | Rename a user |

---

## Frontend (`room.js`)

The frontend is plain JavaScript with no build step or framework. Responsibilities:

- Manage the WebSocket lifecycle (connect, auto-reconnect, close)
- Render participant cards, vote progress, controls, and results panel
- Optimistically update local vote state on card selection
- Persist the user's display name in `sessionStorage` (scoped per room)

---
