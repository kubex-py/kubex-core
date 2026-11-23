# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Until 0.1.0-beta.5, kubex-core lived in the [kubex](https://github.com/kubex-py/kubex) repository
and was released in lock-step with kubex; the notes for those releases are kubex-core's part of
kubex's changelog. From the next release on, kubex-core has its own version numbers, and kubex
depends on a compatible range.

## [Unreleased]

### Added

- `kubex_core.models.admission`: `AdmissionReview`, `AdmissionRequest` and `AdmissionResponse`
  (`admission.k8s.io/v1`) for admission webhooks. `AdmissionReview` and `AdmissionRequest` are
  generic over the request's object type; `AdmissionRequest.allow()`/`deny()` build the response.

### Changed

- kubex-core moved to its own repository, [kubex-py/kubex-core](https://github.com/kubex-py/kubex-core),
  with its history.

## [0.1.0-beta.5] - 2026-11-17

### Added

- Free-threaded Python 3.14t and 3.15t support (beta).

### Fixed

- A resource class first used from several threads at once builds its list model only once.

## [0.1.0-beta.4] - 2026-10-28

### Added

- `kubex_core.models.types`: `Time`, `MicroTime`, `Quantity`, `NullAsEmptyList`,
  `NullAsEmptyDict`.
- `ObjectMetadata.managed_fields`/`self_link` and `ListMetadata.shard_info`, with the
  `ManagedFieldsEntry` and `ShardInfo` models (previously in the generated packages).
- The distribution includes the MIT `LICENSE` file.

### Fixed

- Unknown fields round-trip through resource models instead of being dropped on replace.
- `MicroTime` always serializes six fractional digits; naive datetimes serialize as UTC.
- `Quantity` fields accept numbers.
- Default plurals for custom resources (`Gateway` → `gateways`, `Mesh` → `meshes`).
- A subclass of a resource model gets its own list model.
- A list whose `items` is `null` parses as an empty list.
- `Status` bodies without `metadata` parse.
- `Scale` at 0 replicas parses (the API server omits `replicas`).

## [0.1.0-beta.3] - 2026-10-23

### Added

- Python 3.15 support.
- `PartialObjectMetadata` has a `ResourceConfig` (`meta.k8s.io/v1`).

### Fixed

- `ResourceConfig.__get__` no longer mutates the shared instance inherited by `BaseEntity`
  subclasses without their own `__RESOURCE_CONFIG__`.
- `Status.message` and `Status.status` are optional.

### Changed

- **Breaking:** Python 3.10 is no longer supported; the minimum is now 3.11.
- **Breaking:** `WatchEvent`, `EventType`, and `Bookmark` moved from
  `kubex_core.models.watch_event` to kubex (`kubex.core.watch_event`).

## [0.1.0-beta.2] - 2026-05-12

No changes to kubex-core; released in lock-step with kubex 0.1.0-beta.2.

## [0.1.0-beta.1] - 2026-05-06

First beta, released in lock-step with kubex 0.1.0-beta.1.

## [0.1.0-alpha.1] - 2026-04-19

First release: the base models and types shared by kubex and the generated `kubex-k8s-*`
packages, split out of kubex.

[unreleased]: https://github.com/kubex-py/kubex-core/compare/v0.1.0-beta.5...HEAD
[0.1.0-beta.5]: https://github.com/kubex-py/kubex-core/compare/v0.1.0-beta.4...v0.1.0-beta.5
[0.1.0-beta.4]: https://github.com/kubex-py/kubex-core/compare/v0.1.0-beta.3...v0.1.0-beta.4
[0.1.0-beta.3]: https://github.com/kubex-py/kubex-core/compare/v0.1.0-beta.2...v0.1.0-beta.3
[0.1.0-beta.2]: https://github.com/kubex-py/kubex-core/compare/v0.1.0-beta.1...v0.1.0-beta.2
[0.1.0-beta.1]: https://github.com/kubex-py/kubex-core/releases/tag/v0.1.0-beta.1
[0.1.0-alpha.1]: https://pypi.org/project/kubex-core/0.1.0a1/
