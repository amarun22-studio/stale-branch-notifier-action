# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability in the Stale Branch Notifier action, **please do not open a public issue**. Instead, please report it responsibly to the maintainers.

### How to Report
1. **Email**: Send a detailed report to [@amarun22](https://github.com/amarun22) via GitHub direct message or email if available
2. **GitHub Advisory**: Use GitHub's [private vulnerability reporting](https://docs.github.com/en/code-security/security-advisories/guidance-on-reporting-and-writing-information-about-vulnerabilities/privately-reporting-a-security-vulnerability) feature
3. **Please include**:
   - Description of the vulnerability
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if available)

### Response Timeline
- **Acknowledgment**: Within 48 hours
- **Assessment**: Within 7 days
- **Fix/Patch**: Prioritized based on severity
- **Disclosure**: After fix is released

---

## Security Considerations

### What This Action Does
- ✅ Reads branch information from your repository
- ✅ Creates GitHub Issues (requires `issues: write` permission)
- ✅ Reads open PRs (requires `pull-requests: read` permission)
- ✅ Reads repository topics and settings (requires `contents: read` permission)

### What This Action Does NOT Do
- ❌ Never deletes branches (only reads metadata)
- ❌ Never modifies branch protection rules
- ❌ Never executes user code
- ❌ Never stores data outside your repository
- ❌ Never accesses private/sensitive repository data beyond branch info

### Permissions Model
This action requires minimal permissions:
```yaml
permissions:
  contents: read        # read branches and commits
  issues: write         # create and update issues
  pull-requests: read   # read open PRs
```

### Best Practices
When using this action in your workflows:

1. **Use a specific version**: 
   ```yaml
   uses: amarun22-studio/stale-branch-notifier-action@v1  # ✅ Good
   uses: amarun22-studio/stale-branch-notifier-action@latest  # ⚠️ Risky
   uses: amarun22-studio/stale-branch-notifier-action@main  # ❌ Not recommended
   ```

2. **Review logs**: Check workflow logs to verify expected branch scanning behavior

3. **Test with dry-run**: Always test with `dry_run: true` first
   ```yaml
   - uses: amarun22-studio/stale-branch-notifier-action@v1
     with:
       dry_run: true  # Preview without creating issues
   ```

4. **Restrict watchers**: Only CC users who need visibility
   ```yaml
   watchers: your-team,engineering-lead  # Not: everyone
   ```

---

## Known Limitations

### Rate Limiting
- GitHub API rate limits apply (60 req/min for unauthenticated, 5000/hour for authenticated)
- Large repositories (1000+ branches) may trigger rate limiting
- Use a GitHub App token or Personal Access Token for higher limits

### Execution Time
- Action timeout: 15 minutes per workflow run
- Large repositories may exceed this timeout
- Recommended: No more than 2000 branches per repository

### Scope
- Only scans the current repository (no cross-repo scanning)
- Only reads public branch data

---

## Security Updates

### Receiving Notifications
- Watch this repository for security updates (click **Watch** → **Custom** → **Security alerts**)
- Subscribe to [GitHub's security advisories](https://github.com/advisories?query=repo%3Aamarun22-studio%2Fstale-branch-notifier-action)

### Applying Updates
```bash
# Update to latest patch version
uses: amarun22-studio/stale-branch-notifier-action@v1

# Or pin to specific version
uses: amarun22-studio/stale-branch-notifier-action@v1.0.2
```

---

## Dependencies

This action has **zero runtime dependencies** beyond:
- Node.js built-in modules (`fs`, `path`)
- GitHub Actions provided APIs (`github`, `core`, `context`)

No external npm packages are installed during execution.

---

## Responsible Disclosure

We believe in responsible vulnerability disclosure. If you find a security issue:

1. **Do not** disclose it publicly until we've had time to fix it
2. **Do** give us reasonable time to respond and prepare a fix
3. **Do** report all details needed to understand and reproduce the issue
4. **Do expect** timely acknowledgment and regular updates

---

## Questions?

- 🔒 **Security concern**: Contact [@amarun22](https://github.com/amarun22) privately
- 📖 **General security questions**: [GitHub Discussions](https://github.com/amarun22-studio/stale-branch-notifier-action/discussions)
- 🐛 **Found a bug**: [Open an issue](https://github.com/amarun22-studio/stale-branch-notifier-action/issues)

---

**Last updated**: April 13, 2026
