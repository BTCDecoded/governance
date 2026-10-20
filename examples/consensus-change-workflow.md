# Consensus Change Workflow

## Overview

**Critical distinction:** This document describes a written review schedule. It does not decide what enters the repository. The app posts a `governance/merge` status and can ask GitHub whether a pull request is mergeable. It does not merge the pull request. Users decide whether to run a release.

## Phases

### Phase 1: Proposal (Before PR)

**Duration:** Variable (weeks to months)

**Steps:**
1. Research and design (identify problem, research solutions, design change, consider Bitcoin principles)
2. Community discussion (GitHub Discussion in blvm-spec repo, present solution, engage feedback)
3. Write BIP specification (draft BIP, include motivation/specification/rationale, submit to bitcoin-dev)
4. Create test vectors (comprehensive test cases, edge cases, reference implementations)
5. An equivalence proof is not a merge check. `verify_behavioral_equivalence` returns success when `expected_result` is non-empty, and the comment says the check is simulated. It does not prove mathematical correctness.
6. A security audit is not a merge check. `get_tier_requirements` can include the text "Security audit report attached to PR". The merge webhook does not read that list. `EmergencyTier::Critical` sets `requires_security_audit` and a 60-day deadline, and production source does not call that module.

### Phase 2: Pull Request (status post, not repository approval)

**Duration:** `get_review_period_for_layer` returns 180 days for layers 1 and 2. It does not return 365.

**Requirements the merge path actually reads:**
- A count of stored signature rows against the 6-of-7 table
- That 180-day review flag
- The webhook posts `governance/merge`. It does not check a BIP, test vectors, a security audit, or an equivalence proof.

**Steps:**

1. **Open Pull Request**
   - Target: `blvm-spec` or `blvm-consensus` repository
   - Title: `[CONSENSUS] BIP-XXX: <description>`
   - Link to BIP, tests, proof, audit

2. **Governance App Validation**
   - Tier number: ```blvm-commons/src/validation/tier_classification.rs:classify_pr_tier()```. A database override can replace that tier. There is no `classify_tier` function.
   - Review period used: ```blvm-commons/src/validation/threshold.rs:get_review_period_for_layer()``` returns 180 for layers 1 and 2, not 365
   - Layer threshold: ```blvm-commons/src/validation/threshold.rs:get_threshold_for_layer()``` returns 6-of-7 for layers 1 and 2
   - There is no `check_required_artifacts`. `security_controls.rs` maps changed files to configured controls. The `security-gate` binary can call `analyze_security_impact`. The merge webhook does not.

3. **Technical Review** (Ongoing)
   - Maintainers review code quality, test coverage, specification adherence, security implications, equivalence proof

4. **Community Review** (Public)
   - Open to all developers and users, GitHub PR comments, mailing list discussion, independent implementations encouraged

5. **Security Audit** (not a merge check)
   - The merge function does not read an audit report. `verify_security_property` searches for the substrings `break_consensus`, `validate`, and `bypass_security`.

6. **Maintainer Signatures**
   - The comment command is `/governance-sign <signature>`, with an optional quoted reason.
   - The signed message is `PR #{number} in {repo}`. It does not include a commit hash, a BIP number, or a timestamp.
   - `verify_governance_signature` checks that signature against the maintainer key before the row is stored. A missing GitHub review is logged and does not block. `check_signatures` later counts the stored rows.

7. **Review Period Elapses**
   - The threshold function's layer 1-2 period is 180 days. If `emergency_mode` is passed true, that same function returns 30 for every layer. The webhook passes false.

8. **Status posted**
   - `should_block_merge` turns the two flags into a `governance/merge` status
   - That status does not enable the merge. Branch protection leaves `enforce_admins` false, and a failed protection update still returns success.

**At this point:** A status may have been posted. That does not make the change a network consensus rule, and it does not by itself merge the pull request.

### Phase 3: Not a release step

The governance crate does not merge a pull request into `blvm-node`, compile release binaries, or publish an announcement. A `governance/merge` status does not make code available for download.

### Phase 4: Fork-detector grace period

**Duration:** The fork detector's default grace period is 30 days, not 90. After that interval from the last detection, `check_time_based_triggers` can execute pending forks. It is not a 90-day measurement of user signaling.

**Nature:** That timer is inside the governance process. It is not an advisory window, and it does not measure Bitcoin network adoption.

**Steps:**
1. Node operators evaluate (review BIP, read audit, test in dev environments, assess risks/benefits)
2. Voluntary upgrade (operators choose independently, economic incentives influence choice)
3. Stored adoption weights, not BIP9 signaling
   - `calculate_adoption_metrics` divides weights in the `fork_decisions` table by the sum of weights in that same table. A row with `node_type` `mining_pool` is counted as the hashpower weight.
   - Default `ForkThresholds` are 50% adoption weight, 10 nodes, 30% mining-pool weight, and 40% other weight. They are not 75% of nodes or 90% of network hash power.
4. Community discussion (ongoing debate, user feedback, bug reports, coordination)

**At this point:** The fork table may contain stored weights. That is not a measurement of Bitcoin network signaling.

### Phase 5: In-process ruleset swap

**Nature:** `perform_fork_transition` updates the ruleset held by this process. It is not a user vote and not a network activation.

| Outcome | What the code does |
|---------|--------------------|
| Thresholds met | `perform_fork_transition` replaces `current_ruleset` in the process with another governance ruleset. It does not change Bitcoin consensus rules, and it does not read miner signals. |
| Thresholds not met | The current ruleset stays. A maintainer signature does not put code into the repository. |

There is no soft-fork or hard-fork outcome in this path. A signature count does not activate a network consensus change.

## Example Timeline

| Month | Activity |
|-------|----------|
| 0 | Community discussion begins |
| 3 | BIP drafted and submitted |
| 6 | No audit is scheduled by this crate. |
| 9 | Pull request opened (coded review is 180 days, not a 365-day clock) |
| 12 | No audit is marked complete. The merge path does not read an audit report. |
| 15 | Maintainer signatures accumulate |
| 21 | Signature rows may meet 6-of-7. That posts a status. It does not enable the merge, and the review function does not measure 365 days. |
| 22 | A status may have been posted. The app does not merge the pull request. |
| 24 | A release is a separate publish step. This table does not perform it. |
| 28-39 | There is no coded network-activation clock. `perform_fork_transition` only replaces the in-process governance ruleset. |

**Total:** This table is not a clock the code runs.

**Why the old 39-month figure was here:** It was a story about network activation. The layer 1-2 review value in `get_review_period_for_layer` is 180 days. The fork path does not wait 39 months, and it does not activate consensus rules.

## Historical Comparisons

| Change | Timeline | Lesson |
|--------|----------|--------|
| **SegWit** (2015-2017) | 2015: BIP141 proposed → 2017 August: Activated | Users ultimately decided, despite developer/miner disagreements |
| **Taproot** (2018-2021) | 2018: Initial proposals → 2021 November: Activated | Uncontroversial changes activate faster, but still took ~3 years |
| **SegWit2x** (2017) | 2017: Proposed → 2017: Cancelled before activation | Corporate/miner support insufficient without user buy-in |

## Common Questions

| Question | Answer |
|----------|--------|
| Can maintainers force a consensus change? | No. The app posts a `governance/merge` commit status. That status does not stop a merge. Branch-protection updates set `enforce_admins` to false, and a failed update still returns success. Maintainers do not control network adoption. |
| What if maintainers approve a change users reject? | A stored signature row does not put the change into the repository. The app posts a status. It does not merge the pull request. A merge, if someone with GitHub write access makes one, is still not network activation. |
| What if users want a change maintainers reject? | A public GitHub fork of these repositories is a GitHub feature, not a governance action. `ForkExecutor` switches a governance ruleset when its own adoption counters pass thresholds, and `execute_fork` is private. There is no user-activated soft fork coordinator in this tree. |
| Why does the prose say 365 days for consensus changes? | `get_review_period_for_layer` returns 180 for layers 1 and 2. The only 365 in `blvm-commons` is a key lifetime. |
| Can emergency mode bypass the coded review? | The webhook passes `emergency_mode: false`. If that flag is true, `get_review_period_for_layer` returns 30 for every layer, including 1 and 2. |
| What about emergency bug fixes in consensus code? | The schedule in `src/validation/emergency.rs` is Critical 0 days and 4-of-7, Urgent 7 days and 5-of-7, Elevated 30 days and 6-of-7. Production source does not call that module. The callers are tests. The merge webhook passes `emergency_mode: false`. |
| How is this different from Bitcoin Core? | Bitcoin Core's CONTRIBUTING.md names repository maintainers who merge pull requests, run the release cycle in `doc/release-process.md`, and moderate. It also says there is no privileged class of Bitcoin Core developers. BTCDecoded writes multisig counts and posts a `governance/merge` status. That status does not stop a merge, and admin enforcement is left off. |

## Best Practices

| For Proposers | For Maintainers | For Users |
|---------------|-----------------|-----------|
| Start with discussion, not code | Review rigorously (extreme scrutiny) | Participate early (comment, test, provide feedback) |
| Document thoroughly (BIP, test vectors, rationale) | Communicate clearly (explain decisions, maintain transparency) | Evaluate independently (read BIPs, don't defer to authority) |
| Engage critics (opposition feedback improves proposals) | Serve users, not preferences (advisory role, humility essential) | Exercise sovereignty (upgrade when convinced, fork if necessary) |
| Think long-term (permanent changes, 10+ year implications) | | Coordinate carefully (network effects matter, avoid accidental splits) |

## Conclusion

The app posts a `governance/merge` status. That status is not repository approval, and it is not network adoption.

Maintainers can sign a message of the form `PR #{number} in {repo}`. Users decide whether to run a binary.
