# ci_templates
Templates for workflows and CI

## Workflows

- `.github/workflows/reusable_build.yaml` — reusable workflow for `build`, `asan`, and `tsan` CI (configured via `mixin`, `packages`, `dist-matrix`, `ros-distribution`, and `repos-branch-override`).
- `.github/workflows/reusable_asan.yaml` — **deprecated** wrapper around `reusable_build.yaml`; kept for backwards compatibility with older release branches. New and updated workflows should call `reusable_build.yaml` directly with `mixin: asan`.
- `.github/workflows/build.yaml`, `.github/workflows/asan.yaml`, `.github/workflows/triage.yml` — workflows for this repository itself (`build.yaml` and `asan.yaml` self-test the reusable workflows; `triage.yml` adds opened issues/PRs to the org inbox project).
