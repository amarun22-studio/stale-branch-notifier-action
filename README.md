# Stale Branch Notifier Action

Automatically detect and notify about stale feature branches in your GitHub repository. This GitHub Action identifies inactive branches and creates (or updates) GitHub Issues to notify branch owners to take action.

**By:** [Arunkumar Amarnath](https://github.com/amarun22) (@amarun22)  
**Part of:** [amarun22-studio](https://github.com/amarun22-studio)

---

## Overview

This self-contained action scans all branches in your repository, identifies those with no recent commits, and notifies the branch authors via GitHub Issues. It includes:

- ✅ Configurable inactivity threshold
- ✅ Smart collaborator validation
- ✅ Automatic issue creation/updates
- ✅ Automatic reconciliation and stale-issue auto-close
- ✅ Dry-run mode for safe testing
- ✅ Exclude specific branches by policy
- ✅ PR metadata in issue body
- ✅ No dependency on private repositories

Best for:

- repositories that want a lightweight stale-branch policy without a separate app
- teams that want issue-based follow-up instead of immediate branch deletion
- scheduled hygiene checks that still support safe manual dry runs

---

## Quick Start

Add this action to a scheduled workflow and grant the required permissions:

```yaml
name: Stale Branch Check

on:
  schedule:
    - cron: '0 9 * * 0'
  workflow_dispatch:

jobs:
  stale-branches:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      issues: write
      pull-requests: read
    steps:
      - uses: amarun22-studio/stale-branch-notifier-action@v1
        with:
          days_inactive: 15
          dry_run: 'false'
```

If you want centralized configuration, pass repository variables into the inputs.

---

## Requirements

- Issues must be enabled in the target repository.
- The workflow job must grant `contents: read`, `issues: write`, and `pull-requests: read`.
- The action runs with the caller repository token, so it works for repositories where the workflow itself has access.

---

## Usage

### Basic Usage

Add this to your GitHub Actions workflow:

```yaml
- name: Run Stale Branch Notifier
  uses: amarun22-studio/stale-branch-notifier-action@v1
  with:
    days_inactive: 15
    dry_run: false
    watchers: alice,bob
```

### Complete Workflow Example

```yaml
name: Stale Branch Check
on:
  schedule:
    - cron: '0 9 * * 0'  # Every Sunday at 09:00 UTC
  workflow_dispatch:
    inputs:
      days_inactive:
        description: 'Days of inactivity threshold'
        required: false
        default: '15'
      dry_run:
        description: 'Dry run mode (no issues created)'
        required: false
        type: boolean
        default: false

jobs:
  check-stale:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      issues: write
      pull-requests: read
    
    steps:
      - name: Run Stale Branch Notifier
        uses: amarun22-studio/stale-branch-notifier-action@v1
        with:
          days_inactive: ${{ github.event.inputs.days_inactive || '15' }}
          dry_run: ${{ github.event.inputs.dry_run || 'false' }}
          watchers: team-lead,devops-admin
          excluded_branches: main,production,develop
```

---

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `days_inactive` | Days of inactivity threshold | No | `15` |
| `dry_run` | Log actions without creating issues | No | `false` |
| `watchers` | Comma-separated GitHub usernames to CC | No | `` |
| `excluded_branches` | Comma-separated branches to exclude | No | `` |

### Input Details

**`days_inactive`**  
Number of days a branch can be inactive before it's considered stale. Default: 15 days.
```yaml
with:
  days_inactive: 30
```

**`dry_run`**  
When `true`, logs what would happen without creating any GitHub Issues. Perfect for testing.
```yaml
with:
  dry_run: 'true'
```

**`watchers`**  
Comma-separated list of GitHub usernames to receive `@mention` in every issue for visibility.
```yaml
with:
  watchers: alice,bob,charlie
```

**`excluded_branches`**  
Comma-separated list of exact branch names to skip from scanning. The `main` branch is always excluded.
```yaml
with:
  excluded_branches: main,production,release/latest
```

---

## Outputs

| Output | Description |
|--------|-------------|
| `stale_branches_found` | Number of stale branches detected |
| `issues_created` | Number of issues created or updated |
| `issues_auto_closed` | Number of open stale issues auto-closed during reconciliation |

### Using Outputs

```yaml
- name: Run Stale Branch Notifier
  id: notifier
  uses: amarun22-studio/stale-branch-notifier-action@v1
  with:
    days_inactive: 15

- name: Report results
  run: |
    echo "Stale branches found: ${{ steps.notifier.outputs.stale_branches_found }}"
    echo "Issues created: ${{ steps.notifier.outputs.issues_created }}"
    echo "Issues auto-closed: ${{ steps.notifier.outputs.issues_auto_closed }}"
```

---

## Sample Issue Created

When a stale branch is detected, an issue like this is created:

```
[Stale Branch] Action needed: 2 inactive branches — octocat

🌿 Stale Feature Branch — Action Required

Hi @octocat,

The following feature branch(es) associated with your account have had 
no commits for 15+ days and need attention:

| Branch | Last Commit | Inactive For | Open PR(s) |
|--------|-------------|--------------|-----------|
| feature/login-redesign | 2026-03-18 | 23 days | #421 |
| feat/api-v2 | 2026-03-12 | 29 days | None |

### Please take one of these actions for each branch:
- 🔨 Push new commits (work in progress)
- 🔀 Open a Pull Request (ready for review)
- 🗑️ Delete the branch (abandoned)

⚠️ Stale branches add clutter and make navigation harder.

---
📢 CC for visibility: @alice @bob

_Auto-generated by Stale Branch Notifier · 2026-04-13_
```

---

## Advanced Configuration

### Using Repository Variables (Recommended)

Composite actions cannot read the caller repository's `vars` context automatically, so the recommended pattern is to pass repository variables into the action inputs from your workflow:

1. Go to **Settings → Secrets and variables → Variables**
2. Create these variables:
   - `STALE_BRANCH_NOTIFIER_DAYS_INACTIVE` = `15`
   - `STALE_BRANCH_NOTIFIER_WATCHERS` = `alice,bob`
   - `STALE_BRANCH_NOTIFIER_EXCLUDED_BRANCHES` = `main,production`

3. Pass those repository variables into the action inputs in your workflow:
```yaml
- uses: amarun22-studio/stale-branch-notifier-action@v1
  with:
    days_inactive: ${{ vars.STALE_BRANCH_NOTIFIER_DAYS_INACTIVE }}
    watchers: ${{ vars.STALE_BRANCH_NOTIFIER_WATCHERS }}
    excluded_branches: ${{ vars.STALE_BRANCH_NOTIFIER_EXCLUDED_BRANCHES }}
```

Inside this action, precedence is:

1. Action input value supplied by your workflow
2. Built-in default (`15` days for threshold, empty lists for watchers/exclusions)

### Testing with Dry Run

Test the action safely without creating issues:

```yaml
- uses: amarun22-studio/stale-branch-notifier-action@v1
  with:
    days_inactive: 15
    dry_run: 'true'  # Log only, no issues created
```

Check the workflow logs to see what would happen.

---

## Permissions

This action requires the following permissions:

```yaml
permissions:
  contents: read          # Read branch metadata
  issues: write           # Create/update issues
  pull-requests: read     # Read PR information
```

Add these to your workflow or job-level permissions.

---

## How It Works

1. **Scans all branches** - Lists all branches in the repository
2. **Checks last commit** - Determines when each branch was last updated
3. **Identifies stale branches** - Compares against your threshold (default: 15 days)
4. **Validates authors** - Checks if branch author is an active collaborator
5. **Creates/updates issues** - Groups branches by author and creates GitHub Issues
6. **CC watchers** - Mentions configured watchers for visibility
7. **Handles idempotency** - Updates existing issues instead of creating duplicates

---

## Behavior

### Branch Exclusions
- **Default branch** is always excluded (e.g., `main`)
- **Excluded branches** from input are skipped
- **Other branches** are evaluated for staleness

### Author Validation
- **Active collaborators** get assigned the issue
- **Repo owners** with implicit admin access get assigned
- **Deleted/removed authors** → issue assigned to watchers + author info in body
- **External committers** (no GitHub login) → assigned to watchers

### Issue Updates
- **Same stale branch on next run** → Existing issue updated + refresh comment
- **Branch no longer stale** → Issue auto-closed with clear comment
- **Branch deleted** → Issue auto-closed
- **Branch excluded by policy** → Existing stale issue auto-closed as non-actionable

---

## Troubleshooting

### No issues created
- Check if any branches are actually older than your threshold
- Run with `dry_run: true` to see logs
- Verify permissions are set correctly

### Issue not assigned
- Confirm the branch author is an active collaborator
- Check watchers are configured if author is external
- Review workflow logs for validation details

### Workflow fails
- Ensure `contents: read`, `issues: write`, `pull-requests: read` permissions
- Check GitHub token has access to the repository
- Review workflow logs for specific errors

---

## Related Projects

- **[amarun22-studio](https://github.com/amarun22-studio)** - Collection of GitHub Actions and development tools

---

## Contributing

Found a bug? Have a feature request? Issues and pull requests are welcome!

Visit the [GitHub repository](https://github.com/amarun22-studio/stale-branch-notifier-action) for:
- Issue tracking
- Pull request guidelines
- Bug reports and feature requests

---

## License

MIT - see [LICENSE](LICENSE) file

---

## Support

For questions, issues, or feature requests:
- **GitHub:** [@amarun22](https://github.com/amarun22)
- **Issues:** [Open an issue](https://github.com/amarun22-studio/stale-branch-notifier-action/issues)

---

**Made with ❤️ by [Arunkumar Amarnath](https://github.com/amarun22)**
