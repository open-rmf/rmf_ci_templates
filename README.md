# ci_templates
Templates for workflows and CI

## Workflows

- `.github/workflows/reusable_build.yaml` — reusable workflow for `build`, `asan`, and `tsan` CI (configured via `mixin`, `packages`, `dist-matrix`, `ros-distribution`, and `repos-branch-override`).
- `.github/workflows/reusable_asan.yaml` — **deprecated** wrapper around `reusable_build.yaml`; kept for backwards compatibility with older release branches. New and updated workflows should call `reusable_build.yaml` directly with `mixin: asan`.
- `.github/workflows/build.yaml`, `.github/workflows/asan.yaml`, `.github/workflows/triage.yml` — workflows for this repository itself (`build.yaml` and `asan.yaml` self-test the reusable workflows; `triage.yml` adds opened issues/PRs to the org inbox project).

## `reusable_build.yaml` inputs

| Input | Required | Default | Description |
|---|---|---|---|
| `packages` | yes | — | Newline-separated package names to build and test. |
| `mixin` | no | `build` | Build mode: `build` (`ccache`, `coverage-gcc`, `lld`), `asan` (`asan-gcc`, `lld`), or `tsan` (`tsan`, `lld`). |
| `dist-matrix` | no | `humble`, `jazzy`, `lyrical`, `rolling` | JSON array of `{ros_distribution}` entries (`ubuntu_distribution` optional). |
| `ros-distribution` | no | `""` | Optional single ROS distro (`humble`, `jazzy`, `kilted`, `lyrical`, `rolling`); overrides `dist-matrix` when non-empty. |
| `repos-branch-override` | no | `""` | Branch of `open-rmf/rmf` for `rmf.repos`; `""` or `"auto"` uses `matrix.ros_distribution`. |

When `ubuntu_distribution` is omitted, `ros_distribution` auto-maps to:
- `humble` → `jammy`
- `jazzy`, `kilted` → `noble`
- `lyrical`, `rolling` → `resolute`
