# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.2] — 2026-04-13

### Added
- `examples/` directory with three ready-to-use workflow templates:
  - `basic-schedule.yml` — minimal weekly scheduled check
  - `advanced-with-variables.yml` — full config with repo variables, dispatch inputs, and job summary
  - `manual-dry-run.yml` — safe preview workflow for first-time setup and testing
- Repository topics for Marketplace discoverability: `github-actions`, `stale-branches`, `branch-management`, `automation`, `repository-hygiene`

## [1.0.1] — 2026-04-13

### Changed
- README polished for GitHub Marketplace: added Quick Start, Requirements, Advanced Configuration, Troubleshooting, and Behavior sections
- Comprehensive input/output reference with per-field examples

## [1.0.0] — 2026-04-13

### Added
- Initial public release on GitHub Marketplace
- Self-contained composite action — no dependency on private repositories
- Branch scanning via paginated GitHub API with configurable `days_inactive` threshold (default: 15)
- Author validation: checks collaborator permission level; handles deleted users and repo owners
- Issue lifecycle management:
  - Creates or updates one issue per stale-branch author
  - Groups all stale branches by author in a single issue
  - Adds a refresh comment on re-runs (idempotent)
  - Auto-closes stale issues when branches are no longer actionable (deleted, excluded, or active)
- PR metadata included in issue body (open PR count and links per branch)
- `watchers` input: comma-separated usernames CC'd in every issue
- `excluded_branches` input: exact branch names to skip from scanning (`main`/default branch always excluded)
- `dry_run` input: logs all actions without creating or modifying any issues
- Outputs: `stale_count`, `issues_count`, `auto_closed_count`
- MIT License

[Unreleased]: https://github.com/amarun22-studio/stale-branch-notifier-action/compare/v1.0.2...HEAD
[1.0.2]: https://github.com/amarun22-studio/stale-branch-notifier-action/compare/v1.0.1...v1.0.2
[1.0.1]: https://github.com/amarun22-studio/stale-branch-notifier-action/compare/v1.0.0...v1.0.1
[1.0.0]: https://github.com/amarun22-studio/stale-branch-notifier-action/releases/tag/v1.0.0
