# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Until 0.1.0-beta.5, kubex-core lived in the [kubex](https://github.com/kubex-py/kubex) repository
and was released in lock-step with kubex; the notes for those releases are in
[kubex's changelog](https://github.com/kubex-py/kubex/blob/main/CHANGELOG.md). From the next
release on, kubex-core has its own version numbers, and kubex depends on a compatible range.

## [Unreleased]

### Added

- `kubex_core.models.admission`: `AdmissionReview`, `AdmissionRequest` and `AdmissionResponse`
  (`admission.k8s.io/v1`) for admission webhooks. `AdmissionReview` and `AdmissionRequest` are
  generic over the request's object type; `AdmissionRequest.allow()`/`deny()` build the response.

### Changed

- kubex-core moved to its own repository, [kubex-py/kubex-core](https://github.com/kubex-py/kubex-core),
  with its history.

[unreleased]: https://github.com/kubex-py/kubex-core/compare/v0.1.0-beta.5...HEAD
