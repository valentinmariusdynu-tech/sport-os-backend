# sport-os-backend — Stack Conventions

## Stack
- Python 3.11+, FastAPI, SQLAlchemy 2.x, Alembic, PostgreSQL
- Package manager: uv (preferred) or pip + pyproject.toml
- Containerisation: Docker + docker-compose for local dev

## Code Conventions
- Ruff for formatting and linting (`ruff format .` / `ruff check .`)
- Type hints required on all public functions
- Pydantic v2 models for all request/response schemas
- Async by default; sync only for Alembic migrations

## Testing
- pytest + pytest-asyncio + httpx async test client
- Coverage gate: 80 %
- Integration tests hit real Postgres via testcontainers

## Git
- Branches: feat/, fix/, chore/
- Conventional commits (feat:, fix:, chore:, docs:)
- PRs merged via squash; main is protected
