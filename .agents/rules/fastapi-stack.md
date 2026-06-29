# FastAPI Stack Rules

Load this file when creating or modifying FastAPI application code, Python dependencies, runtime commands, async behavior, database integration, settings, caching, logging, WebSocket behavior, task queues, or third-party API integration.

## Python And Dependency Management

- Use `uv` for package and environment management.
- Target Python 3.12 or newer.
- When initializing FastAPI dependencies, use `uv add "fastapi[standard-no-fastapi-cloud-cli]"` so the FastAPI Cloud CLI is not installed.
- Run local Python scripts with `uv run -- <script.py>`.
- Only use `python <script.py>` inside a production image that was built without `uv`.
- Ask the developer before installing, removing, or changing Python dependencies.

## FastAPI

- Use FastAPI for REST API development.
- Start the application with the current official FastAPI CLI style, such as `fastapi run <main.py>`, instead of invoking `uvicorn` directly.
- Use `typing.Annotated` for FastAPI metadata such as path parameters, query parameters, dependencies, and request validation.
- Keep endpoint layers thin. Put reusable business logic in services or modules with clear boundaries.
- Treat authentication, authorization, input validation, and secret handling as first-class design concerns.
- Never store or transmit passwords in plaintext. For password login flows, hash passwords with a suitable algorithm such as Argon2 or bcrypt.

## API Design

- GET endpoints that may return large datasets must support pagination.
- Endpoint error handling must return appropriate HTTP status codes and informative error responses.
- Do not expose internal exception details, secrets, stack traces, or implementation internals in API error responses.
- Calls to third-party APIs must use explicit timeouts.
- Calls to third-party APIs must use exponential backoff retry behavior for transient failures.
- Prefer `tenacity` for retry behavior when a retry library is needed, but ask the developer before adding it as a dependency.

## Async-First Architecture

- Prefer async APIs and libraries throughout the application.
- Do not introduce sync-only components without asking the developer first.
- If a chosen technology is sync-only but appropriate for the task, document the exception and contain it behind a clear boundary.

## Database And Settings

- Use SQLAlchemy with Alembic for relational databases.
- Prefer PostgreSQL for relational database needs.
- Use `asyncpg` as the PostgreSQL driver.
- Use modern SQLAlchemy type annotations such as `Mapped[...]` for mapped columns and relationships.
- Use Pydantic `BaseSettings` for environment-driven configuration.
- Design settings so CI/CD systems and deployment platforms can inject configuration through environment variables.
- Ask the developer before adding database drivers or migration-related dependencies.

## Caching And Logging

- Prefer Redis for caching needs.
- Use Loguru consistently for application logging.
- Ask the developer before adding Redis client libraries, Loguru, or related infrastructure dependencies.

## Realtime And Background Work

- If the project needs WebSocket-style realtime behavior, prefer Socket.IO over raw FastAPI WebSocket primitives unless the developer chooses otherwise.
- Favor Socket.IO when event modeling, automatic reconnects, rooms, broadcasts, or client ecosystem support would reduce custom infrastructure.
- If long-running tasks require a task queue, prefer Celery.
- Before setting up Celery, ask the developer which broker and result backend to use, such as Redis or RabbitMQ.
- Because Celery is sync-oriented, ask the developer before introducing it into an otherwise async-first architecture.

## Optional Architecture

- Consider Clean Architecture only when project scale, domain complexity, or developer preference justifies it.
- Do not force Clean Architecture onto small services where a simpler modular structure is easier to maintain.
