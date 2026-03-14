# Usage Guide

A complete walkthrough of every PockerDeck feature.

---

## Creating a room

1. Open the app (e.g. [http://localhost:8000](http://localhost:8000)).
2. Click **+ Create Room**.  
   You are redirected to a new room with a unique 8-character code (e.g. `a1b2c3d4`).
3. Share the URL or the room code with your team.

---

## Joining a room

Two ways to join:

| Method | Steps |
|--------|-------|
| **Direct URL** | Open the shared link — the app takes you straight to the room. |
| **Room code** | On the home page, enter the code in the *"Join with a code"* field and press **Join →** or `Enter`. |

When you land on the room page for the first time, you are prompted to enter your **display name**. This name is visible to everyone in the room. Your name is remembered per-room using `sessionStorage`, so you won't be asked again if you reload the page.

---

## Voting

Once you have entered the room:

1. Optionally read the **Story** field if the host has set a task description.
2. Click any card from the card grid to cast your vote.

!!! info "Vote privacy"
    Your vote value is kept hidden from others until the host reveals cards. Other participants only see a **✓** (voted) or **…** (not voted yet) badge next to your name.

You can change your vote at any time before the reveal — just click a different card.

---

## Setting a story description

Any participant can type a description of the current story/task in the **Story** text field and press `Enter` (or click outside). The text is broadcast to everyone in the room instantly.

---

## Tracking progress

The progress indicator below the story field shows how many participants have voted:

```
3 of 5 voted
```

---

## Revealing votes

Click **Reveal** to show everyone's votes simultaneously. Once revealed:

- Each participant card displays the **actual vote value**.
- The **Results** panel appears at the bottom showing:
  - **Average** (rounded to one decimal place, excluding `?` and `30+` votes)
  - **Lowest** vote
  - **Highest** vote

!!! tip
    Only numeric values (`3`, `6`, `9` … `30`) are included in the average calculation. `?` and `30+` are shown but excluded.

---

## Starting a new round

After revealing, click **New Round** to:

- Clear all votes
- Reset the revealed state
- Keep the current participants and story description

Everyone's card selection is cleared and the voting panel returns.

---

## Connection status

A small badge in the top-right corner of the room shows your current connection state:

| Badge | Meaning |
|-------|---------|
| 🟢 Connected | WebSocket is live |
| 🔴 Disconnected — reconnecting… | Temporary drop; the client retries automatically every 2.5 s |

If the room no longer exists on the server (e.g. after a restart), you are redirected to the home page with an alert.

---

## Keyboard shortcuts

| Shortcut | Action |
|----------|--------|
| `Enter` in name field | Confirm display name |
| `Enter` in story field | Save story description |
