# Review Expectations

## Overview

This document describes **expected** review practices for maintainers. These are **guidelines**, not enforced requirements. Review quality emerges naturally through merit, community feedback, and the challenge mechanism.

**Key Principle**: We document expectations to help maintainers understand best practices, not to create rigid enforcement mechanisms.

---

## Expected Review Practices

### Before Signing a PR

Maintainers are expected to:

1. **Read the PR**: Understand what changes are being made
2. **Review the code**: Check correctness, security, consensus compliance
3. **Consider impact**: Understand the change's effect on the system
4. **Provide feedback**: Comment if issues are found

**Note**: These are expectations, not requirements. The challenge mechanism provides accountability if reviews are consistently insufficient.

---

## Review Types

### Approved
- Code looks good, ready to merge (after review period)
- No blocking issues found
- May include suggestions for improvement

### Changes Requested
- Issues found that need to be addressed
- PR should not merge until changes are made
- Should include specific feedback on what needs to change

### Commented
- Questions or suggestions (not blocking)
- Code review provided but not blocking merge
- Useful for non-critical feedback

### Dismissed
- Review was dismissed (e.g., outdated after PR changes)
- Not counted as active review

---

## Review Quality Indicators

These are **transparent metrics**, not enforcement:

- **Review comments provided**: Whether the review includes written feedback
- **Review timing**: When the review was submitted relative to PR creation
- **Review depth**: Line-by-line vs. high-level review
- **Signature-review linking**: Whether maintainer reviewed before signing

**Note**: These metrics are published in monthly governance reports. Users can decide if review quality is a problem.

---

## Challenge Mechanism

If a review seems insufficient, anyone can challenge:

```
/governance-challenge insufficient_review <pr_number> "Insufficient review: <reason>" <signature>
```

**Example**:
```
/governance-challenge insufficient_review 123 "Maintainer signed without reviewing code changes" <signature>
```

### Challenge Process

1. **Challenge created**: Cryptographically signed challenge posted
2. **30-day response**: Maintainers must respond within 30 days
3. **Transparent resolution**: All challenges and responses are public
4. **No prescriptive outcome**: Resolution depends on context and community judgment

**Note**: Challenges are a mechanism for conflict resolution, not a weapon. Use them constructively.

---

## Spontaneous Order Principle

Review quality emerges naturally through:

- **Maintainer reputation**: Poor reviews damage reputation
- **Community feedback**: Users can challenge insufficient reviews
- **Challenge mechanism**: Formal process for addressing problems
- **Exit competition**: Forking if reviews are consistently poor
- **Transparent metrics**: Monthly reports show review activity

**We don't enforce review quality - we make it transparent and challengeable.**

---

## What We're NOT Doing

### ❌ Mandatory Review Quality Standards
- **Why**: Central planning - assumes we know "right" review quality
- **Alternative**: Document expectations, let challenges reveal problems

### ❌ Minimum Review Comment Requirements
- **Why**: Prescriptive - doesn't match reality (some reviews are brief)
- **Alternative**: Track comments transparently, enable challenges

### ❌ Review Quality Scoring
- **Why**: Central planning - assumes we can measure "quality"
- **Alternative**: Transparent metrics, let users decide

### ❌ Mandatory Review Checklist
- **Why**: Rigid enforcement, violates spontaneous order
- **Alternative**: Document review expectations (not enforced)

---

## Review-Signature Linking

The governance system tracks whether maintainers reviewed before signing:

- **Transparent tracking**: All signatures show if review exists
- **Not blocking**: Signatures without reviews are logged but not blocked
- **Monthly reports**: Statistics show signatures with/without reviews
- **Challengeable**: Users can challenge if pattern emerges

**Purpose**: Transparency enables users to verify review activity, not to enforce it.

---

## Best Practices

### For Maintainers

- **Review before signing**: Review the PR before posting your signature
- **Provide feedback**: Comment on issues you find, even if not blocking
- **Be constructive**: Helpful feedback improves code quality
- **Respond to challenges**: If challenged, respond within 30 days

### For Contributors

- **Be patient**: Review periods vary by tier (7-180 days)
- **Respond to feedback**: Address review comments promptly
- **Challenge if needed**: Use challenge mechanism if review seems insufficient
- **Understand expectations**: Reviews are expected but not rigidly enforced

---

## See Also

- [GOVERNANCE.md](GOVERNANCE.md) - Complete governance model
- [METRICS.md](METRICS.md) - Monthly governance reports with review statistics
- [CONTRIBUTOR_GUIDE.md](CONTRIBUTOR_GUIDE.md) - Contributor paths and options
- [HOW_TO.md](HOW_TO.md) - Step-by-step governance instructions

---

**Remember**: Review expectations are guidelines, not requirements. The challenge mechanism and transparent metrics provide accountability without prescriptive enforcement.

