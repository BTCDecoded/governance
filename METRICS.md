# Governance Metrics

Monthly governance reports are published automatically to provide transparency about governance activity.

## Report Contents

Each monthly report includes:

### Merge Distribution
- Total number of merges in the period
- Breakdown by maintainer (count and percentage)
- Enables users to see if power is concentrated

### PR Statistics
- Total PRs opened
- Merged, pending, and rejected counts
- Breakdown by governance tier (1-5)
- Shows review activity and tier distribution

### Challenge Statistics
- Total challenges created
- Pending, resolved, and rejected counts
- Shows conflict resolution activity

### Maintainer Activity
- PRs merged by each maintainer
- Signatures given (approvals)
- Challenges created
- Challenges resolved
- Sorted by total activity

## Access

Reports can be generated using the `governance-report` binary:

```bash
# Generate report for current month
DATABASE_URL=sqlite:governance.db cargo run --bin governance-report

# Generate report for specific month
DATABASE_URL=sqlite:governance.db cargo run --bin governance-report -- --month 2025-01

# Output as Markdown
DATABASE_URL=sqlite:governance.db cargo run --bin governance-report -- --format markdown

# Save to file
DATABASE_URL=sqlite:governance.db cargo run --bin governance-report -- --output report.json
```

Reports are published monthly at: `governance/reports/YYYY-MM.json`

## Purpose

**Transparency enables users to:**
- Verify governance is working as intended
- Decide if problems exist (e.g., power concentration)
- Make informed decisions about forking
- Hold maintainers accountable through visibility

## Important Note

These are **transparent metrics**, not **enforcement mechanisms**.

- **No prescriptive limits**: We don't enforce "no maintainer can merge more than X%"
- **User decision**: Users decide if concentration is a problem
- **Exit competition**: Forking provides the check on power
- **Spontaneous order**: Merit-based selection emerges naturally

**We publish metrics to enable informed decisions, not to mandate outcomes.**

## Principles Alignment

### Ostrom (#4: Monitoring)
- Transparent metrics enable users to monitor governance
- All data is publicly accessible and verifiable

### Hayek (Spontaneous Order)
- No central planning of "correct" distribution
- Users decide what's acceptable through exit competition
- Metrics reveal problems, don't enforce solutions

### Cypherpunk (Don't Trust, Verify)
- All metrics are cryptographically verifiable
- Data comes from immutable audit logs
- Users can verify reports independently

## Report Format

Reports are available in two formats:

### JSON
Machine-readable format for programmatic analysis:
```json
{
  "period_start": "2025-01-01T00:00:00Z",
  "period_end": "2025-01-31T23:59:59Z",
  "merge_distribution": {
    "total_merges": 42,
    "by_maintainer": [
      {
        "username": "alice",
        "count": 25,
        "percentage": 59.5
      }
    ]
  },
  ...
}
```

### Markdown
Human-readable format for documentation:
```markdown
# Governance Report

**Period**: 2025-01-01 to 2025-01-31

## Merge Distribution
...
```

## Using Metrics

### For Users
- Review monthly reports to understand governance activity
- Compare periods to see trends
- Use data to make informed decisions about participation

### For Maintainers
- See your own activity and contributions
- Understand overall governance health
- Identify areas needing attention

### For Researchers
- Analyze governance patterns over time
- Compare with Bitcoin Core governance
- Study power concentration and distribution

## See Also

- [GOVERNANCE.md](GOVERNANCE.md) - Complete governance model
- [CONTRIBUTOR_GUIDE.md](CONTRIBUTOR_GUIDE.md) - Contributor paths and options
- [HOW_TO.md](HOW_TO.md) - Step-by-step governance instructions

---

**Remember**: Metrics are tools for transparency and verification, not enforcement mechanisms. Users retain sovereignty to fork, run alternatives, or reject changes based on this information.






