# CLAUDE.md — sport-os-backend

## Purpose
FastAPI backend for Sport-OS: auth, athlete profiles, events, telemetry ingestion, and APIs consumed by sport-os-mobile and sport-os-ai.

## Stack
- Python 3.11, FastAPI, Pydantic v2
- SQLAlchemy 2 (async), Alembic
- PostgreSQL 16, Redis (cache + pub/sub)
- uv (package manager), Docker Compose (local dev)

## Key Directories
- `app/api/v1/` — route handlers by domain
- `app/core/` — pydantic-settings config, JWT, DI
- `app/models/` — SQLAlchemy ORM models
- `app/schemas/` — Pydantic v2 request/response schemas
- `app/services/` — business logic; never called directly from routes without a service layer
- `tests/` — pytest, httpx AsyncClient, factory_boy

## Dev Commands
```bash
uv run uvicorn app.main:app --reload
uv run pytest
uv run ruff check . --fix
uv run mypy app/
uv run alembic upgrade head
```

## Conventions
- `async def` throughout; no sync DB calls in async routes
- Never return ORM models directly — always use a Pydantic schema
- Secrets via pydantic-settings from `.env`; never hardcode
- All endpoints under `/api/v1/`
- Services raise `HTTPException` for domain errors

## Related Repos
- [sport-os-mobile](https://github.com/valentinmariusdynu-tech/sport-os-mobile) — primary API consumer
- [sport-os-ai](https://github.com/valentinmariusdynu-tech/sport-os-ai) — calls telemetry endpoints
- [sport-os-infra](https://github.com/valentinmariusdynu-tech/sport-os-infra) — K8s/Terraform deploy config