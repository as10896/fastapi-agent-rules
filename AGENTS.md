# Agent Instructions

These instructions apply to coding agents working in this repository. Keep all code, comments, commit messages, and project documentation in English unless the developer explicitly requests otherwise. Conversation with the developer may follow the language they use.

## Mandatory Rules

- Plan first for non-trivial work. Break the goal into clear tasks, explain the intended approach, and wait for developer approval before implementing when the task is broad, ambiguous, architectural, or likely to touch multiple files.
- Inspect relevant files before editing. Follow existing project patterns instead of inventing a new structure.
- Keep changes small and focused. Do not modify unrelated files, reformat unrelated code, or revert changes you did not make unless explicitly asked.
- Prefer the simplest maintainable implementation. Avoid overengineering and do not add abstractions unless they reduce real complexity or match an established project pattern.
- Follow modular design and SOLID principles. Keep boundaries clear and put behavior where it naturally belongs.
- Treat API design as security-sensitive by default. Never store or transmit passwords in plaintext; use appropriate password hashing such as Argon2 or bcrypt for password-based authentication.
- Use async-first architecture. If a required library or component is sync-only, ask the developer before introducing that exception.
- Do not add, remove, or upgrade dependencies without developer approval. If a third-party library would materially simplify a complex task, explain the trade-off and ask first.
- Use available project, documentation, or context helpers when they improve confidence. Ask the developer before installing external agent skills, tools, or rule packs.
- Never hard-code secrets, credentials, tokens, or local machine paths. Do not commit `.env`; only `.env.example` may be committed, and it must contain keys with empty values.
- Every completed task must include a validation loop. Run the narrowest relevant tests and checks, review the resulting diff, and do not mark work complete while known errors remain.
- If validation cannot be run, clearly state what was not verified and why.

## Default Preferences

- Use `uv` for Python dependency and environment management. Target Python 3.12 or newer.
- Use FastAPI for REST APIs.
- Prefer pytest for unit and integration tests.
- Use Ruff for Python formatting and linting after code generation or Python edits.
- Use SQLAlchemy with Alembic when the project requires a relational database; prefer PostgreSQL with `asyncpg` as the driver.
- Use Pydantic `BaseSettings` for environment-based configuration.
- Prefer Redis for caching.
- Use Loguru for application logging.
- Prefer Dockerized development and deployment workflows designed for CI/CD and CaaS platforms such as Cloud Run, Railway, or Heroku.
- Write complete type annotations throughout the Python codebase.
- Add concise docstrings when they improve readability. Keep code comments rare, useful, and in English.
- Follow current official best practices for third-party libraries.
- Prefer modern library syntax recommended by official documentation, such as `Annotated` for FastAPI parameter metadata and `Mapped[...]` for SQLAlchemy models.

## External Rule Loading

The files under `.agents/rules/` contain detailed guidance. They are intentionally not imported automatically so agents can avoid unnecessary context.

- Do not preload every referenced rule file.
- Read a rule file only when the task touches that area.
- Treat a loaded rule as mandatory unless it conflicts with explicit developer instructions or the mandatory rules above.
- Follow references recursively only when needed for the current task.
- Reference detailed rule files with plain paths only. Do not create at-prefixed imports or include-style references.

Relevant detailed rules:

- FastAPI stack, dependency choices, async-first constraints, and modern syntax: `.agents/rules/fastapi-stack.md`
- Validation loop, pytest, AnyIO, Ruff, and local checks: `.agents/rules/testing-validation.md`
- Docker, Compose, container security, and CI/CD deployment assumptions: `.agents/rules/deployment.md`
- New project bootstrap expectations for `.gitignore`, `.env.example`, settings, and README: `.agents/rules/project-bootstrap.md`

## Workflow

1. Clarify or plan before implementation when requirements are unclear.
2. Read the smallest useful set of files and any relevant `.agents/rules/*.md` details.
3. Implement focused changes that match the existing project style.
4. Add or update tests when behavior changes and doing so is practical.
5. Run the narrowest relevant validation commands.
6. Review the diff for regressions, unrelated edits, secrets, and accidental churn.
7. Summarize changed files and validation results.
