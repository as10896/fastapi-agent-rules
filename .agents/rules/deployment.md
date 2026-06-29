# Deployment And Container Rules

Load this file when creating or modifying Dockerfiles, Compose files, deployment configuration, CI/CD workflows, runtime commands, or container health checks.

## Deployment Direction

- Dockerize the application by default.
- Design Docker and deployment configuration with future CI/CD automation in mind.
- Assume the service may be deployed to a CaaS platform such as Cloud Run, Railway, or Heroku.
- Keep build steps reproducible and suitable for automated image builds.

## Dockerfile

- Use a multi-stage Dockerfile to keep the final image small.
- In the build stage, prefer the official `uv` image to install Python dependencies.
- In the production stage, use a lightweight Python base image and copy only the prepared virtual environment from the build stage.
- The production image does not need to include `uv`.
- Do not run the application as root inside the container.
- Keep the Dockerfile focused on building the image. Avoid embedding orchestration-only concerns.

## Compose

- Name the Docker Compose file `compose.yaml`, not `docker-compose.yaml`.
- Put container health checks in `compose.yaml`, not in the Dockerfile.
- Keep Compose suitable for local development while avoiding hard-coded secrets.

## Runtime Commands

- In local development, use `uv run -- <script.py>` for Python scripts.
- In the production image, where `uv` is intentionally absent, use the image's Python runtime directly.
- Prefer the FastAPI CLI style, such as `fastapi run <main.py>`, for starting the FastAPI application.

## Security And Configuration

- Never bake secrets into images or Compose files.
- Inject configuration through environment variables.
- Use `.env.example` for documenting required variables, with empty values only.
- Avoid local machine paths in deployment files.
