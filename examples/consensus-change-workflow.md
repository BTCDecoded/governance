# Consensus Change Workflow

## Overview

**Critical Distinction:** This workflow governs **repository approval** (what enters BTCDecoded code), not **network adoption** (what Bitcoin runs). Maintainers approve code for release. Users decide whether to run it.

## Phases

### Phase 1: Proposal (Before PR)

**Duration:** Variable (weeks to months)

**Steps:**
1. Research and design (identify problem, research solutions, design change, consider Bitcoin principles)
2. Community discussion (GitHub Discussion in blvm-spec repo, present solution, engage feedback)
3. Write BIP specification (draft BIP, include motivation/specification/rationale, submit to bitcoin-dev)
4. Create test vectors (comprehensive test cases, edge cases, reference implementations)
5. Write equivalence proof (prove mathematical correctness for blvm-consensus layer)
6. Security audit planning (identify auditors, define scope, budget, timeline, disclosure plan)

### Phase 2: Pull Request (Repository Approval)

**Duration:** 365 days minimum

**Requirements:**
- 6-of-7 maintainer signatures
- 365-day review period
- BIP specification approved
- Test vectors comprehensive
- Security audit passed
- Equivalence proof validated

**Steps:**

1. **Open Pull Request**
   - Target: `blvm-spec` or `blvm-consensus` repository
   - Title: `[CONSENSUS] BIP-XXX: <description>`
   - Link to BIP, tests, proof, audit

2. **Governance App Validation**
   - Detects consensus rule change: ```blvm-commons/src/validation/tier_classification.rs:classify_tier()```
   - Applies 365-day review: ```blvm-commons/src/validation/threshold.rs:get_review_period_for_layer()```
   - Requires 6-of-7 threshold: ```blvm-commons/src/validation/threshold.rs:get_threshold_for_layer()```
   - Checks required artifacts: ```blvm-commons/src/validation/security_controls.rs:check_required_artifacts()```

3. **Technical Review** (Ongoing)
   - Maintainers review code quality, test coverage, specification adherence, security implications, equivalence proof

4. **Community Review** (Public)
   - Open to all developers and users, GitHub PR comments, mailing list discussion, independent implementations encouraged

5. **Security Audit** (Required)
   - Professional security firm review, vulnerability assessment, report published, issues addressed before merge

6. **Maintainer Signatures**
   - Each maintainer signs when satisfied: `/governance-sign <signature>`
   - Signature includes PR hash, BIP number, timestamp
   - Cryptographically verified

7. **Review Period Elapses**
   - 365 days from PR opening (cannot be shortened, even with emergency mode)

8. **Merge Enabled**
   - All requirements met (signatures + time)
   - Code enters BTCDecoded repository

**At This Point:** Repository approval complete. Code is officially BTCDecoded consensus rules.

### Phase 3: Release (Optional Upgrade Available)

**Steps:**
1. Integration testing (merge into blvm-node, test with real-world scenarios, verify backward compatibility)
2. Release build (compile binaries, create release notes, document new consensus rules)
3. Release announcement (publish on website, post to bitcoin-dev, social media)
4. Optional upgrade available (users can download, no forced upgrades, old versions remain available)

**At This Point:** Code is available. Users begin evaluating.

### Phase 4: User Signaling (Advisory)

**Duration:** 90+ days (measurement period)

**Nature:** Advisory, not mandatory. Maintainers cannot force adoption.

**Steps:**
1. Node operators evaluate (review BIP, read audit, test in dev environments, assess risks/benefits)
2. Voluntary upgrade (operators choose independently, economic incentives influence choice)
3. Signaling measurement (BIP9-style version bits or node polling)
   - Metrics: Node adoption %, hash power signaling %, economic activity (exchanges, wallets)
   - Recommended thresholds: 75% node adoption, 90% hash power, economic majority
4. Community discussion (ongoing debate, user feedback, bug reports, coordination)

**At This Point:** Network signaling indicates support level. Users remain in control.

### Phase 5: Activation Decision (User Sovereignty)

**Nature:** Users decide, not maintainers.

| Outcome | Description | Result |
|---------|-------------|--------|
| **Soft Fork** | Sufficient support, economic majority, miners signal | Consensus rules change network-wide, backward compatible |
| **Hard Fork** | Contentious change, no clear majority, competing visions | Users choose chain, markets decide value, both chains may survive |
| **Rejection** | Insufficient support, economic majority opposes, miners don't signal | Network continues with old rules, maintainer-approved code unused |

**Key Point:** No amount of maintainer signatures forces adoption. Users govern Bitcoin.

## Example Timeline

| Month | Activity |
|-------|----------|
| 0 | Community discussion begins |
| 3 | BIP drafted and submitted |
| 6 | Security audit planned |
| 9 | Pull request opened (365-day clock starts) |
| 12 | Security audit completed |
| 15 | Maintainer signatures accumulate |
| 21 | All signatures received (6-of-7), 365 days elapsed, merge enabled |
| 22 | Merged, integrated into blvm-node |
| 24 | Release published |
| 25-27 | User evaluation period |
| 28-30 | Node upgrade phase (90-day signaling) |
| 33 | Sufficient support achieved |
| 36 | Activation date set by community |
| 39 | Network-wide activation |

**Total:** ~39 months (3.25 years) from discussion to activation

**Why so long?** Bitcoin's $2T network cap demands extreme caution. Consensus changes are permanent and irreversible.

## Historical Comparisons

| Change | Timeline | Lesson |
|--------|----------|--------|
| **SegWit** (2015-2017) | 2015: BIP141 proposed → 2017 August: Activated | Users ultimately decided, despite developer/miner disagreements |
| **Taproot** (2018-2021) | 2018: Initial proposals → 2021 November: Activated | Uncontroversial changes activate faster, but still took ~3 years |
| **SegWit2x** (2017) | 2017: Proposed → 2017: Cancelled before activation | Corporate/miner support insufficient without user buy-in |

## Common Questions

| Question | Answer |
|----------|--------|
| Can maintainers force a consensus change? | No. Maintainers control repository merge access, not network adoption. |
| What if maintainers approve a change users reject? | Change enters BTCDecoded code but doesn't activate on network. Unused code. |
| What if users want a change maintainers reject? | Users can fork BTCDecoded, use alternative implementations, or coordinate UASF. |
| Why 365 days for consensus changes? | Bitcoin's $2T network demands extreme caution. Allows thorough review, verification, ecosystem preparation, user education. |
| Can emergency mode bypass 365-day review? | No. Emergency mode doesn't apply to consensus changes. Consensus changes require long timelines by design. |
| What about emergency bug fixes in consensus code? | Critical bugs use emergency tiers (0-30 days) but still require multi-signature approval. These restore *intended* consensus rules, not change them. |
| How is this different from Bitcoin Core? | Bitcoin Core has no formal governance. BTCDecoded formalizes repository governance with multi-signature requirements but maintains advisory-only relationship with network. |

## Best Practices

| For Proposers | For Maintainers | For Users |
|---------------|-----------------|-----------|
| Start with discussion, not code | Review rigorously (extreme scrutiny) | Participate early (comment, test, provide feedback) |
| Document thoroughly (BIP, test vectors, rationale) | Communicate clearly (explain decisions, maintain transparency) | Evaluate independently (read BIPs, don't defer to authority) |
| Engage critics (opposition feedback improves proposals) | Serve users, not preferences (advisory role, humility essential) | Exercise sovereignty (upgrade when convinced, fork if necessary) |
| Think long-term (permanent changes, 10+ year implications) | | Coordinate carefully (network effects matter, avoid accidental splits) |

## Conclusion

BTCDecoded governance provides structure for repository management while preserving user sovereignty for protocol changes.

**Repository approval ≠ Network adoption**

Maintainers propose. Users dispose.
