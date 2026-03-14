# Contributing

Thank you for your interest in improving PockerDeck! Contributions of all kinds are welcome — bug reports, feature requests, documentation fixes, and code changes.

---

## Code of conduct

Please be respectful and constructive in all interactions. We follow the [Contributor Covenant](https://www.contributor-covenant.org/) code of conduct.

---

## Reporting bugs

Before opening a new issue:

1. Search the [existing issues](https://github.com/byteavanta/pockerdeck/issues) to avoid duplicates.
2. If no existing issue covers your problem, [open a new one](https://github.com/byteavanta/pockerdeck/issues/new).

A good bug report includes:

- A clear, descriptive title
- Steps to reproduce the problem
- Expected vs. actual behaviour
- Browser / OS / Docker version (if relevant)

---

## Suggesting features

Open a [GitHub Discussion](https://github.com/byteavanta/pockerdeck/discussions) or an issue labelled `enhancement`. Describe:

- The problem you are trying to solve
- Your proposed solution
- Any alternatives you considered

---

## Development setup

### 1. Fork & clone

```bash
git clone https://github.com/<your-username>/pockerdeck.git
cd pockerdeck
```

### 2. Create a branch

Use a short, descriptive branch name:

```bash
git checkout -b fix/reconnect-loop
# or
git checkout -b feat/dark-mode
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the dev server

```bash
cd app
uvicorn main:app --reload
```

The app is available at [http://localhost:8000](http://localhost:8000). The `--reload` flag restarts the server automatically on source changes.

---

## Making changes

### Backend (`app/main.py`)

- Keep the file self-contained — no new external dependencies unless absolutely necessary.
- All WebSocket actions must be handled safely: validate and sanitise every field received from the client.
- Add or update the relevant doc page in `pockerdeck-doc` if your change affects user-visible behaviour.

### Frontend (`app/static/js/room.js`, `app/templates/`)

- No build step, no framework — plain HTML / CSS / JavaScript only.
- Keep the UI accessible: prefer semantic HTML elements and meaningful button labels.

### Docker

- Test your changes inside the container before submitting:

```bash
docker compose up --build
```

---

## Submitting a pull request

1. **Rebase** your branch on the latest `main`:

    ```bash
    git fetch origin
    git rebase origin/main
    ```

2. **Run a quick smoke test** — open the app, create a room, vote with two browser tabs, reveal, and reset.

3. **Push** your branch and open a PR against `main`:

    ```bash
    git push origin <your-branch>
    ```

4. Fill in the PR template:
    - What does this change do?
    - How was it tested?
    - Screenshots (for UI changes)

!!! tip
    Keep PRs focused. One logical change per PR makes review faster and keeps the git history clean.

---

## Contributing to the documentation

The documentation lives in a separate repository: [byteavanta/pockerdeck-doc](https://github.com/byteavanta/pockerdeck-doc).

```bash
git clone https://github.com/<your-username>/pockerdeck-doc.git
cd pockerdeck-doc
pip install -r requirements.txt
mkdocs serve
```

Preview at [http://localhost:8000](http://localhost:8000). Submit fixes as a PR to `main` in that repo — the GitHub Actions workflow deploys it to GitHub Pages automatically.

---
