# qr-redirect

A self-hostable, dynamic QR code redirect service built with Flask. Create short redirect links and generate QR codes that can be updated without reprinting.

## Tech Stack

- Python 3.12
- Flask
- SQLAlchemy (via Flask-SQLAlchemy)
- Flask-Login
- Flask-Migrate (Alembic)
- SQLite (default; swappable via `SQLALCHEMY_DATABASE_URI`)
- uv (dependency management)

## Status

In development - see roadmap below.

## Setup

### With uv (recommended)

```bash
git clone <repo-url> qr-redirect
cd qr-redirect
uv sync
cp .env.example .env   # then edit .env with your values
uv run flask --app app run
```

### Without uv (fallback)

```bash
git clone <repo-url> qr-redirect
cd qr-redirect
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install -e .
cp .env.example .env        # then edit .env with your values
flask --app app run
```

## Configuration

| Variable | Description | Default |
|---|---|---|
| `SECRET_KEY` | Flask secret key, set to a long random string in production | `dev-secret-key` |
| `SQLALCHEMY_DATABASE_URI` | Database connection string | `sqlite:///app.db` |
| `REDIRECT_DOMAIN` | Public domain used when building QR code URLs (e.g. `https://go.example.com`) | *(empty)* |
| `FLASK_APP` | Entry point for the Flask CLI | `app` |
| `FLASK_DEBUG` | Enable debug mode (`1` = on, `0` = off) | `1` |

## Project Structure

```
qr_redirect/
├── app/
│   ├── __init__.py        # Flask app factory
│   ├── config.py          # Config classes
│   ├── models.py          # SQLAlchemy models
│   ├── routes/
│   │   ├── __init__.py
│   │   ├── auth.py        # Auth routes
│   │   ├── redirects.py   # Redirect CRUD + redirect route
│   │   └── admin.py       # Admin panel routes
│   ├── templates/
│   └── static/
├── tests/
├── .env.example
├── .gitignore
├── LICENSE
├── pyproject.toml
└── README.md
```

## Roadmap

1. **Auth**: user registration, login, logout via Flask-Login; session management
2. **Redirect CRUD + redirect route**: create/edit/delete redirect entries; `/<slug>` route that resolves and redirects
3. **QR generation + admin panel**: on-demand QR code PNG generation per redirect; admin dashboard with click stats
4. **Docker + CLI tools + polish**: Dockerfile and Compose file; CLI commands for seeding/export; production hardening

## License

MIT. See [LICENSE](LICENSE).
