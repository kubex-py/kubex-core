# kubex-core

Base Pydantic models and types shared by kubex (kubex-py/kubex) and the generated
`kubex-k8s-*` packages. Split out of the kubex workspace with its history (`kubex_core/`
was `packages/kubex-core/kubex_core/`, and before that `kubex/models/`).

## Commands

- `uv sync`: environment with the dev group
- `uv run pytest`: tests (in `tests/`)
- `uv run ruff check .` / `uv run ruff format .`
- `uv run mypy kubex_core tests`: strict, with the pydantic plugin

`uv.lock` is committed; CI syncs with `--locked`, so run `uv lock` after changing dependencies.

## Constraints

- Runtime dependencies stay minimal: `pydantic>=2.0,<3` (the 2.0 floor is deliberate) and pyyaml.
  Never depend on kubex or a generated package at runtime; kubex depends on this package.
- Python 3.11–3.15, including free-threaded 3.14t/3.15t: shared state must be thread-safe
  without the GIL (see the list-model builder in `resource_config.py`).
- Changes here reach every generated package. Breaking changes need a minor version bump
  (`0.X`), since dependents pin `>=X.Y,<X.(Y+1)`.

## Releases

Own semver. Bump `version` in `pyproject.toml`, update `CHANGELOG.md`, merge, then push a
`vX.Y.Z` tag on `main`: `publish.yml` checks the tag against the built version and publishes
to PyPI. Every pull request from this repository publishes a `.devN` build to TestPyPI.

CI and the build go through the reusable workflows in kubex-py/.github.
