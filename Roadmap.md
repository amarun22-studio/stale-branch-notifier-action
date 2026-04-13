# Roadmap

A glimpse into the future of the Stale Branch Notifier action. This roadmap is **not a guarantee**, but rather a reflection of the planned direction based on user feedback and community needs.

---

## 📋 Current Version: v1.0.2

### ✅ Completed Features
- ✅ Automatic stale branch detection
- ✅ GitHub Issues-based notifications
- ✅ Author validation and assignment
- ✅ Dry-run mode for safe testing
- ✅ Configurable inactivity threshold
- ✅ Branch exclusion support
- ✅ PR metadata in issue body
- ✅ Automatic reconciliation / stale-issue auto-close
- ✅ GitHub Marketplace distribution
- ✅ Branch protection on main
- ✅ Validation CI workflow

---

## 🎯 Planned for v1.1 (Near-term)

### 🔔 Slack Notifications
**Goal:** Notify via Slack instead of (or in addition to) GitHub Issues  
**Reason:** Teams often prefer real-time Slack alerts  
**Difficulty:** Medium  
**Est. Timeline:** Q2 2026

### 📧 Email Notifications
**Goal:** Optional email notifications to branch authors  
**Reason:** Ensures visibility for users who don't watch GitHub  
**Difficulty:** Low  
**Est. Timeline:** Q2 2026

### 📊 Stale Branch Dashboard
**Goal:** Summary report of stale branches by team/owner  
**Reason:** Managers need visibility into repo health  
**Difficulty:** Medium  
**Est. Timeline:** Late Q2 2026

---

## 🚀 Planned for v2.0 (Medium-term)

### 🎯 Branch Pattern Matching
**Goal:** Filter stale detection to specific branch patterns  
**Example:** Only report on `feature/*` and `release/*` branches  
**Reason:** Staging/dev branches may not need the same treatment  
**Difficulty:** Low  
**Est. Timeline:** Q3 2026

### 🗑️ Auto-Delete Option
**Goal:** Optionally delete stale branches after N grace days  
**Reason:** Full automation for teams that prefer cleanup  
**Safety:** Must include:
  - Grace period before deletion
  - Dry-run validation
  - Prevent deletion of branches with open PRs
  - Audit trail
**Difficulty:** High  
**Est. Timeline:** Q3-Q4 2026

### 🔗 Multi-Repository Support
**Goal:** Scan multiple repositories with one action  
**Reason:** Org-wide branch hygiene  
**Complexity:** Medium  
**Est. Timeline:** Q3 2026

### 🏷️ Custom Labels & Milestones
**Goal:** Auto-label issues, optionally assign to milestone  
**Reason:** Better issue organization and workflow integration  
**Difficulty:** Low  
**Est. Timeline:** Q2 2026

---

## 💡 Under Consideration (Speculative)

These are ideas we're considering but haven't committed to:

### 🤖 Smart Stale Detection
**Idea:** ML-based staleness detection (e.g., detect abandoned vs actively merged PRs)  
**Challenge:** Requires training data and ongoing maintenance  
**Status:** ❓ Exploring feasibility

### 📈 Trend Reports
**Idea:** Weekly/monthly summary of stale branch trends  
**Example:** "Stale branches ↑ 15% this month"  
**Status:** ❓ User feedback pending

### 🔐 Organization-wide Policies
**Idea:** Define org-level stale branch policies (GitHub App)  
**Challenge:** Requires GitHub App distribution model  
**Status:** ❓ Post-v2.0 consideration

### 🔄 Integration with Branch Protection
**Idea:** Auto-update branch protection rules for stale branches  
**Example:** Auto-block merges to stale branches  
**Status:** ❓ Risk assessment needed

### ⚡ Performant Large-Scale Scanning
**Idea:** Optimize for repositories with 5000+ branches  
**Challenge:** Current approach works for 2000 branches  
**Status:** ⏳ Performance-dependent

---

## 📅 Timeline Overview

```
Q1 2026
  └─ v1.0.0-v1.0.2 published ✅

Q2 2026
  ├─ v1.1: Slack/Email, Custom Labels ⏳
  └─ v2.0 preview: Pattern matching

Q3 2026
  ├─ v2.0: Auto-delete, Multi-repo
  └─ Trend reports

Q4 2026+
  └─ Post-v2.0: Org policies, ML, integrations
```

---

## 🗣️ Community Input

**Your feedback shapes this roadmap.** Please:

1. **Vote on features**: React 👍 to [issues](https://github.com/amarun22-studio/stale-branch-notifier-action/issues) you'd find useful
2. **Suggest features**: Open a [feature request](https://github.com/amarun22-studio/stale-branch-notifier-action/issues/new?template=feature_request.md)
3. **Share use cases**: [Start a discussion](https://github.com/amarun22-studio/stale-branch-notifier-action/discussions) about how you use this action
4. **Report blockers**: If anything prevents you from using v1.0, [open an issue](https://github.com/amarun22-studio/stale-branch-notifier-action/issues/new?template=bug_report.md)

---

## 🤝 Contributing to the Roadmap

Want to help build these features? We welcome contributions!

- **Developers**: See [CONTRIBUTING.md](CONTRIBUTING.md)
- **Ideas**: Share your thoughts in [Discussions](https://github.com/amarun22-studio/stale-branch-notifier-action/discussions)
- **Bug reports**: [Report issues](https://github.com/amarun22-studio/stale-branch-notifier-action/issues/new?template=bug_report.md)

---

## 📝 Notes

- All timelines are **estimates** and subject to change
- **v1.x** focuses on stability and core features
- **v2.0** planned for major enhancements
- Roadmap updated quarterly based on feedback and priorities

---

**Last updated:** April 13, 2026  
**Maintained by:** [@amarun22](https://github.com/amarun22)
