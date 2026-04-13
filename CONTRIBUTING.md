# Contributing to Stale Branch Notifier

Thanks for your interest in contributing! This document explains how to set up your development environment, run tests, and submit changes.

---

## Getting Started

### Prerequisites
- Git
- Node.js 18+
- GitHub CLI (`gh`)
- Bash/shell

### Setup
```bash
# Clone the repository
git clone https://github.com/amarun22-studio/stale-branch-notifier-action.git
cd stale-branch-notifier-action

# Create a feature branch
git checkout -b feat/your-feature-name

# Make your changes
```

---

## Development Workflow

### 1. Make Your Changes
Edit the files you want to modify. Key files:
- `action.yml` — Action metadata and inputs
- `src/notifier.js` — Core logic
- `README.md` — Documentation
- `.github/workflows/validate.yml` — Validation CI

### 2. Test Your Changes Locally
```bash
# Validate action.yml syntax
bash .github/workflows/validate.yml  # or manually check

# Check Node.js syntax
node -c src/notifier.js

# Review your changes
git diff
```

### 3. Test on a Real Repository
1. Push your branch to GitHub
2. Use the test workflow in your own sandbox repo:
   ```yaml
   - uses: your-fork/stale-branch-notifier-action@your-branch
   ```
3. Verify the action behaves as expected

### 4. Commit with Conventional Messages
Use conventional commit format:
```
feat: add new feature
fix: resolve issue
docs: update documentation
test: add test cases
ci: update workflow
refactor: improve code structure
```

Example:
```bash
git commit -m "feat: add support for custom branch patterns"
```

### 5. Create a Pull Request
```bash
# Push your branch
git push origin feat/your-feature-name

# Create PR
gh pr create --title "feat: your feature" --body "Description of changes"
```

---

## Code Style

### JavaScript (src/notifier.js)
- Use clear variable names
- Add comments for complex logic
- Follow existing code patterns
- ESLint/Prettier: Not currently enforced, but follow these patterns:
  - 2-space indentation
  - Single quotes for strings
  - Semicolons required
  - No console logs except during debugging

### Markdown (docs)
- Line length: ~80 characters where possible
- Use descriptive link names (`[Read more](url)` not `[click here](url)`)
- Code blocks with language tags: ` ```yaml `, ` ```javascript `

### YAML (workflows)
- 2-space indentation
- Clear step names
- Comments for non-obvious logic

---

## Branch Protection Rules

This repository uses **strict branch protection**:

- ✅ PR required (cannot push directly to main)
- ✅ Status checks must pass (`Validate Action / validate-action`)
- ✅ Linear history enforced (squash commits on merge)
- ✅ Force pushes not allowed

**What this means for you:**
1. Create a feature branch
2. Push and create a PR
3. Validation workflow runs automatically
4. Once it passes, PR can be merged
5. Your commits are squashed into main

---

## Testing Your Changes

### Validation Workflow
The CI automatically validates:
- ✅ `action.yml` syntax
- ✅ `src/notifier.js` Node.js syntax
- ✅ Required fields in action metadata

### Manual Testing
1. **On a test repo** with simulated stale branches (use the test workflow from `branch-hygiene-bot` repo)
2. **Dry-run mode**: Set `dry_run: true` to preview without creating issues
3. **Full test**: Set `dry_run: false` and verify issues are created properly

---

## Documentation

### Editing README.md
If you change functionality:
- Update the "Inputs" section
- Update the "Outputs" section
- Update "Usage" examples
- Add a section in "Behavior" if adding new logic

### Updating CHANGELOG.md
For any changes, add an entry under `## [Unreleased]`:
```markdown
## [Unreleased]

### Added
- New feature or capability

### Fixed
- Bug fix

### Changed
- Breaking change or modification

### Deprecated
- Feature being phased out
```

---

## Reporting Issues

### Bug Reports
Use the [🐛 Bug Report](https://github.com/amarun22-studio/stale-branch-notifier-action/issues/new?template=bug_report.md) template.

Include:
- Clear description of the problem
- Steps to reproduce
- Your workflow YAML
- Logs/error messages
- Expected vs actual behavior

### Feature Requests
Use the [✨ Feature Request](https://github.com/amarun22-studio/stale-branch-notifier-action/issues/new?template=feature_request.md) template.

Include:
- Clear description of the feature
- Use case / problem it solves
- Proposed solution
- Example workflow usage

### Discussions
For general questions or discussions, use [GitHub Discussions](https://github.com/amarun22-studio/stale-branch-notifier-action/discussions).

---

## Attribution

All contributors will be recognized in the `CHANGELOG.md` file and listed in the repository.

---

## Code of Conduct

Please note that this project is released with a Contributor Code of Conduct. By participating in this project you agree to abide by its terms. Be respectful and constructive in all interactions.

---

## Questions?

- 📚 **Setup help**: See the [README](README.md)
- 💬 **General questions**: [GitHub Discussions](https://github.com/amarun22-studio/stale-branch-notifier-action/discussions)
- 🐛 **Found a bug**: [Open an issue](https://github.com/amarun22-studio/stale-branch-notifier-action/issues)
- 👤 **Direct contact**: [@amarun22](https://github.com/amarun22)

---

**Thank you for contributing!** 🙏
