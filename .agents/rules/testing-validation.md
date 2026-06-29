# Testing And Validation Rules

Load this file when writing tests, changing Python code, choosing validation commands, or diagnosing failed checks.

## Universal Validation Loop

Every task must end with a validation loop before it is considered complete:

1. Implement the focused code or documentation change.
2. Add or update tests when behavior changes and doing so is practical.
3. Run the narrowest relevant tests or checks.
4. Run formatting, linting, or type checks that apply to the changed files.
5. Review the diff for regressions, unrelated edits, accidental churn, and secrets.

Do not mark a task complete while known errors remain. If a check cannot be run, report the skipped check and the reason.

## Pytest

- Prefer pytest for unit and integration tests.
- Write tests so they can run cleanly in CI.
- For async pytest tests, use `@pytest.mark.anyio`.
- Configure the AnyIO backend as `"asyncio"`.
- Do not add `pytest-asyncio` when the project already depends on `fastapi[standard-no-fastapi-cloud-cli]`; FastAPI's standard dependency set already includes AnyIO-related support.
- If pytest is needed and not installed, ask the developer before adding it.

## Ruff

- After generating or editing Python code, run Ruff formatting and linting for the narrowest relevant scope.
- Prefer project-defined commands when they exist. If no project command exists, use direct Ruff commands through `uv run`.
- Fix lint and formatting issues introduced by the change before marking the task complete.

## Choosing Checks

- For a narrow code change, run the smallest test file or test selection that covers the behavior.
- For shared behavior, run broader unit or integration tests that cover affected call paths.
- For documentation-only changes, runtime tests are not required; validate by checking content accuracy, internal consistency, links or paths, and coverage against the source material.
- For Mermaid diagrams or generated structured content, validate syntax when a local validator is available.

## Reporting Validation

In the final response, summarize:

- Which files changed.
- Which tests or checks were run.
- Any checks that could not be run.
- Any remaining risk or follow-up that the developer should know about.
