# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

"Spendly" — a Flask expense tracker built as a step-by-step teaching project. Currently only the marketing/auth-form shell exists; most functionality is intentionally stubbed.

## Commands

```bash
source venv/bin/activate
pip install -r requirements.txt     # flask, werkzeug, pytest, pytest-flask
python app.py                       # dev server on http://localhost:5001 (debug=True)
pytest                              # run tests (none exist yet)
pytest path/to/test_file.py::test_name   # single test
```

No linter or build step is configured.

## Architecture

- `app.py` — single Flask app with all routes. Implemented routes only render templates (`/`, `/register`, `/login`, `/terms`, `/privacy`). Routes `/logout`, `/profile`, `/expenses/add`, `/expenses/<id>/edit`, `/expenses/<id>/delete` are placeholders returning strings, labelled with the tutorial step ("Step 3", "Step 4", "Step 7–9") that will implement them. Note `/register` and `/login` are GET-only; no form handling or sessions yet.
- `database/db.py` — currently only a comment spec: it is to provide `get_db()` (SQLite connection with `row_factory` and foreign keys on), `init_db()` (`CREATE TABLE IF NOT EXISTS`), and `seed_db()`. `expense_tracker.db` is gitignored.
- `templates/` — Jinja templates extending `base.html` (navbar, `title`/`head`/`content` blocks). Link between pages with `url_for(...)`.
- `static/css/style.css` — single stylesheet (fonts: DM Serif Display / DM Sans via Google Fonts); `static/js/main.js` is essentially empty. The landing page's YouTube modal script lives in `templates/landing.html`.

## Conventions

- Commit messages are prefixed by area, e.g. `landing: add privacy policy page and route`.
- Keep placeholder routes' step labels intact when implementing neighbours; replace a placeholder only when implementing that step.
