# FastAPI Agent Rules

My personal agent rules for FastAPI projects 🤘

Across most of my FastAPI projects, I kept running into the same decisions around tech stack, coding style, async-first architecture, validation, Docker layout, and agent workflow. I distilled those repetitive choices into a personal base setup that I can copy into new repositories.

These rules reflect <mark>my own preferences</mark> instead of a universal standard. Use them as a starting point if they fit your workflow, and adapt or ignore anything that does not.

> [!WARNING]
>
> I am actively experimenting with and testing these agent rules. They are not guaranteed to be stable or reliable yet 🥶. If you have suggestions or spot something that could be better, feedback is very welcome!

## Structure

- `AGENTS.md` contains the always-on rules that an AI coding agent should read by default.
- `.agents/rules/fastapi-stack.md` contains detailed FastAPI, dependency, async, database, realtime, and task queue guidance.
- `.agents/rules/testing-validation.md` contains testing, Ruff, and validation-loop details.
- `.agents/rules/deployment.md` contains Docker, Compose, container security, and CI/CD deployment guidance.
- `.agents/rules/project-bootstrap.md` contains new-project setup expectations for version control, settings, environment files, and README structure.

The root `AGENTS.md` intentionally stays concise. Detailed rule files are referenced with plain paths and are meant to be read only when relevant to the current task.

## Design Notes

The split is designed around three categories:

- Hard rules: always-on instructions such as planning first for non-trivial work, validating every completed task, avoiding secrets, and asking before dependency changes.
- Default preferences: common FastAPI project choices such as `uv`, FastAPI, pytest, Ruff, SQLAlchemy/Alembic, Pydantic settings, Docker, and modern type annotations.
- On-demand details: longer guidance stored under `.agents/rules/` so agents can load it only when the task touches that area.

The rule files do not use frontmatter because they are intended to be plain Markdown and tool-agnostic. Cursor-specific `.mdc` rules can be added later if explicit Cursor-only scoping is needed.

## Compatibility

`AGENTS.md` is intended for coding harnesses that support the [AGENTS.md](https://agents.md/) convention, including tools such as Codex, OpenCode, and Cursor.

Different tools handle external references differently. For portability, the rules use plain paths such as `.agents/rules/fastapi-stack.md` instead of `@`-prefixed imports. This keeps detailed rule files as lazy-loading guidance instead of relying on tool-specific import behavior.

> [!NOTE]
>
> I've tested lazy loading with OpenCode many times and it did work. See this [OpenCode conversation](https://opncd.ai/share/2aZcRGUz) for an example where the agent loaded detailed rule files only when the task required them.

For a future Claude Code setup, prefer either:

- a thin `CLAUDE.md` that imports or mirrors the root `AGENTS.md`, or
- a generated/synced `CLAUDE.md` based on `AGENTS.md`.

Keep the detailed `.agents/rules/*.md` references as plain paths unless you intentionally want Claude Code to eager-load them.

## Usage

Copy `AGENTS.md` and the `.agents/` directory into the root of a FastAPI project.

Your coding agents should start from `AGENTS.md`. When a task touches a specific topic, they should then read the matching detailed rule file under `.agents/rules/`.

Treat this as a base setup rather than a complete rule set for every FastAPI project. It captures the patterns I repeat most often, so each project should extend `.agents/rules/` with project-specific conventions or adjust any defaults that do not fit.

For example, a specific project might add rules for:

- Updating `docs/ERD.mmd` in Mermaid format whenever ORM schemas change and a new migration script is generated.
- Updating `docs/authflow.mmd` in Mermaid format whenever auth flow logic changes.
- Using OpenTelemetry for observability.
- Using circuit breaker patterns to reduce system degradation when external services fail.
- Using optimistic locking to avoid race conditions.
- Using the Saga pattern to handle distributed transactions.
- ...

I expect these rules to evolve over time. Repeated agent mistakes usually reveal instructions that are missing, too vague, too broad, or too noisy, so updating the rules should be treated as part of adapting the base setup to each project.
