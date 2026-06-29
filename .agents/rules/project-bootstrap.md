# Project Bootstrap Rules

Load this file when initializing a project, creating repository metadata, adding settings files, writing README content, or preparing environment variable documentation.

## Version Control

- Create and maintain a `.gitignore`.
- Exclude common Python cache and build artifacts such as `__pycache__/`.
- Exclude sensitive files such as `.env`.
- Never commit `.env`.
- Commit `.env.example` when environment variables are needed.
- `.env.example` may contain variable names only; values must be empty.

## Settings

- Use Pydantic `BaseSettings` for application configuration.
- Load configuration from environment variables so CI/CD tools and deployment platforms can inject settings cleanly.
- Do not hard-code secrets, tokens, credentials, or local machine paths.

## README

When initializing a new project, create or update `README.md` with this structure:

- Project Overview: explain the project's purpose and main functionality.
- Prerequisites: mention Docker and Docker Compose.
- Setup Steps: explain how to copy `.env.example` to `.env` and fill in required settings.
- Build: include `docker compose build`.
- Running the Application: include `docker compose up`.
- Testing: include the concrete unit test command for the project.

## Documentation Language

- Write project documentation in English unless the developer explicitly requests another language.
- Keep setup instructions concrete and runnable.
- Prefer documenting project-specific commands over generic background information.
