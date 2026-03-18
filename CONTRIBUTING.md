# Contributing

## Running locally

### Prerequisites

- Python 3.10+
- [uv](https://docs.astral.sh/uv/) (recommended) or pip

### Setup

```bash
git clone https://github.com/aleksandr-miheichev/v2rayn-guide.git
cd v2rayn-guide

# With uv
uv sync --extra docs
uv run mkdocs serve

# With pip
pip install -r requirements-docs.txt
mkdocs serve
```

Open http://127.0.0.1:8000 — the site rebuilds automatically when you edit files.

### Making changes

1. Fork the repo
2. Create a branch: `git checkout -b fix/my-change`
3. Edit files in `docs/ru/` and/or `docs/en/`
4. Check locally with `uv run mkdocs serve`
5. Commit and push
6. Open a Pull Request

### Adding screenshots

Screenshots go in `docs/assets/images/<section>/`.
Use PNG format, crop to ~800–1200px width, show only the relevant part of the window.

### Translations

- Russian docs: `docs/ru/`
- English docs: `docs/en/`

Both have identical structure. When editing content, update both languages if possible.

### Build for production

```bash
uv run mkdocs build --strict
```

Output goes to `site/` — this is what GitHub Actions deploys automatically.
