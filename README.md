# kubex-core

[![CI](https://github.com/kubex-py/kubex-core/actions/workflows/ci.yaml/badge.svg)](https://github.com/kubex-py/kubex-core/actions/workflows/ci.yaml)
[![PyPI](https://img.shields.io/pypi/v/kubex-core)](https://pypi.org/project/kubex-core/)

Shared foundation types for [kubex](https://github.com/kubex-py/kubex) and its generated Kubernetes
resource packages (`kubex-k8s-*`).

Contains:

- `kubex_core.models.base.BaseK8sModel` — Pydantic base with camelCase aliasing.
- `kubex_core.models.base_entity.BaseEntity` — base class for all K8s resources.
- `kubex_core.models.interfaces` — marker interfaces (`NamespaceScopedEntity`, `ClusterScopedEntity`, `HasLogs`, `HasStatusSubresource`, `HasScaleSubresource`, `Evictable`, `HasEphemeralContainers`, `HasResize`, `HasExec`, `HasAttach`, `HasPortForward`).
- `kubex_core.models.resource_config` — `ResourceConfig` descriptor + `Scope`.
- `kubex_core.models.metadata` — `ObjectMetadata`, `ListMetadata`, `OwnerReference`.
- `kubex_core.models.list_entity`, `partial_object_meta`, `status`, `scale`.
- `kubex_core.models.admission` — `AdmissionReview`, `AdmissionRequest`, `AdmissionResponse` (`admission.k8s.io/v1`) for admission webhooks.

This package is a runtime dependency of the `kubex` client and every generated resource package.
End users generally install `kubex` + one `kubex-k8s-*` of choice; this package is pulled in
transitively. Documentation: https://kubex.codemageddon.me/

## Versioning

kubex-core has its own version numbers. kubex and the generated packages depend on a compatible
range (`kubex-core>=X.Y,<X.(Y+1)`), so a kubex-core release doesn't force a kubex release.

## Development

```bash
uv sync
uv run pytest
uv run ruff check . && uv run ruff format --check .
uv run mypy kubex_core tests
```

The tests use real generated models from `kubex-k8s-1-35` (a dev dependency, resolved against
this checkout). CI runs on Python 3.11–3.15 and the free-threaded 3.14t and 3.15t. See the
[contributing guide](https://github.com/kubex-py/.github/blob/main/CONTRIBUTING.md).
