# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- Manual-only release workflow `.github/workflows/release-manual.yml` to automate version tag creation, optional major-tag updates, and GitHub release publishing via `workflow_dispatch`
- Optional IssueOps `/delete-branch <branch>` command: delete a stale branch from an issue comment with full safety checks (branch must be in issue table, not policy-protected, no open PRs)
- Diff summary baked into every stale-branch issue at creation time: commits ahead/behind the default branch, files changed (+additions/-deletions), and a link to the full diff on GitHub — no command needed
- Permission model: issue assignee, configured watchers (`STALE_BRANCH_NOTIFIER_WATCHERS`), and collaborators with write/maintain/admin access are authorized; all others are rejected with a comment
- Policy protection: default branch and `excluded_branches` list cannot be deleted via IssueOps
- Remaining-branch awareness: issue stays open if other branches from the same issue are still alive; closes automatically only when all are resolved
- New example workflow `examples/issueops-delete-branch.yml` for the `issue_comment` trigger with `pull-requests: read` permission

### Changed
- README wording now explicitly frames IssueOps delete as optional, and the sample issue content now includes the default diff summary section

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
