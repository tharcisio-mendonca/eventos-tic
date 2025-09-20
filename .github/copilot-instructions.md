# Copilot Instructions for AI Coding Agents

## Project Overview
This is a Flask-based web application for managing technology events, designed for both web and API usage, with a strong focus on observability, scalability, and production-readiness (Kubernetes, Prometheus, Docker).

## Architecture & Key Components
- **src/main.py**: Application entry point; initializes Flask, routers, logging, DB, and metrics.
- **core/**: Core utilities (database connection, logging, settings management).
- **models/**: SQLAlchemy models (e.g., `event.py` for the Event entity).
- **schemas/**: Pydantic schemas for validation and serialization.
- **services/**: Business logic (e.g., `event_service.py` for event operations).
- **routers/**: Flask Blueprints for API (`api_router.py`) and web pages (`page_router.py`).
- **templates/** & **static/**: Jinja2 HTML templates and static assets (CSS/JS).
- **k8s/**: Kubernetes manifests for deployment and Prometheus integration.
- **dashboard/**: Grafana dashboard JSONs for monitoring.
- **tests/**: Pytest-based tests (see `tests/services/test_event_service.py`).

## Developer Workflows
- **Local development**: Use a Python 3.11+ venv, install from `requirements.txt`, run with `python main.py`.
- **Testing**: Run `pytest` from the `src/` directory. Test files are under `src/tests/`.
- **Docker**: Build with `docker build -t encontros-tech .` and run with `docker run ...` (see README for env vars).
- **Kubernetes**: Apply manifests in `k8s/` with `kubectl apply -f k8s/`.
- **Observability**: Metrics at `/metrics`, health at `/health`, logs are structured and configurable.

## Project-Specific Patterns & Conventions
- **Event Editing**: Uses unique edit tokens (not user auth) for secure event modification (see `models/event.py`, `routers/api_router.py`).
- **Config**: All config via environment variables (see `.env.example` and `core/settings.py`).
- **Logging**: Structured, level-configurable, supports colored output for dev (see `core/logging.py`).
- **API & Web Separation**: API endpoints under `/api/`, web pages under `/` and `/events/`.
- **Validation**: All input/output via Pydantic schemas (`schemas/event.py`).
- **Database**: PostgreSQL via SQLAlchemy, connection string in `DATABASE_URL` env var.
- **Prometheus**: Uses `prometheus-flask-exporter` for metrics, supports multiprocess mode.

## Integration Points
- **PostgreSQL**: Required for all persistent data.
- **Prometheus**: Scrapes `/metrics` for app and business metrics.
- **Grafana**: Dashboards in `dashboard/board.json`.
- **Kubernetes**: Manifests in `k8s/` for deployment and monitoring.

## Examples
- To add a new event field: update `models/event.py`, `schemas/event.py`, and relevant templates/routes.
- To add a new API endpoint: create a function in `routers/api_router.py`, register it in `main.py`, and add tests in `tests/`.

## References
- See `README.md` for full setup, environment variables, and workflow details.
- Use `core/`, `services/`, and `routers/` as primary extension points for new features.

---
For questions or unclear conventions, review `README.md` or ask for clarification.
