# PockerDeck Documentation

Source for the [PockerDeck](https://github.com/byteavanta/pockerdeck-doc) documentation site, built with [MkDocs Material](https://squidfunk.github.io/mkdocs-material/).

## Local development

```bash
pip install -r requirements.txt
mkdocs serve
```

Open [http://localhost:8000](http://localhost:8000) to preview the docs.

## Build

```bash
mkdocs build
```

## Deploy

Documentation is automatically deployed to GitHub Pages via the GitHub Actions workflow in `.github/workflows/deploy.yml` on every push to `main`.
