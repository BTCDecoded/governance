# Governance Scope

## Overview

BTCDecoded governance operates on two levels: **Repository Governance** (a `governance/merge` status) and **Protocol Governance** (advisory).

## Repository Governance (a status post)

| What We Control | What We Don't Control |
|-----------------|----------------------|
| A `governance/merge` commit status. `can_merge_pull_request` only reads GitHub's `mergeable` flag. | Bitcoin's consensus rules (immutable) |
| The webhook posts a review-period status and a signature status. It does not call `check_verification_status`. | Network upgrade activation mechanisms |
| Release creation and versioning | User adoption decisions |
| `RemovalManager::remove_maintainer` sets `maintainers.active` false in SQLite when the caller supplies enough approval ids. Production code does not call it, and it does not change GitHub membership. There is no selection function. | Miner signaling and hash power |
| `required_pull_request_reviews` is null. `check_signatures` counts stored signature rows and posts a status. | Which software users choose to run |
| The webhook posts a review-period status from `get_combined_requirements`. `check_review_period` passes `emergency_mode: false`, so the 30-day emergency reduction in `validate_review_period` is not used. | Node operator configuration choices |
| The pull-request webhook does not call `check_verification_status` or `security-gate`. `check_verification_status` looks for the GitHub check names `Unit & Property Tests` and `Clippy Linting` when another caller reaches it. | Economic decisions and market behavior |

## Protocol Governance (Advisory)

| What We Influence | What We Cannot Do |
|-------------------|-------------------|
| The webhook posts a review-period status and a signature count. It does not score code quality. | Force network adoption (no amount of signatures forces upgrades) |
| User education (documentation, upgrade paths, trade-offs) | Prevent users from running alternative software |
| Nostr is off in `config/app.toml` and in `NostrConfig::default`. The pull-request webhook does not run a technical analysis. | Control economic incentives or market forces |
| | Override user choice (users remain sovereign) |

## Examples

| Scenario | Repository Governance (Can Do) | Protocol Governance (Cannot Do) |
|----------|-------------------------------|--------------------------------|
| Consensus Rule Change | Count stored signatures against a 6-of-7 table and post a status. The coded review is 180 days, not 365. The merge path does not require a BIP or an audit. | Force users to upgrade, control activation, prevent forks |
| Emergency Security Fix | The merge path passes `emergency_mode: false`. `EmergencyTier::Critical` is a written 0-day, 4-of-7 schedule. Production code does not call it, and it is not 4-of-5. | Force immediate adoption, prevent running vulnerable software |
| New RPC Method | `rpc/**` is a tier-2 pattern. The webhook uses `get_combined_requirements`, which takes the max of the stored layer and that tier. Tier 2 alone is 4-of-5 and 30 days. `require_specification` is set on the rule and is not read. | Force users to use it, control integration, prevent alternatives |

**User Process**: A `governance/merge` success status does not merge the pull request and does not create a release. `handle_release_event` starts only when the release action is `published`. Users evaluate and choose. Users can fork or reject.

## Fork Capability

Users can:
- **Repository Fork**: Fork BTCDecoded repositories, maintain own governance rules
- **Protocol Fork**: Create alternative implementations, maintain different consensus rules
- **Exit Strategy**: Always retain option to exit, no single point of failure

## Safeguards and Limitations

| Safeguards | Limitations |
|------------|-------------|
| `set_required_status_checks` sends `enforce_admins: false` and `required_pull_request_reviews: null`. A failed protection update still returns success. | Cannot override Bitcoin's design (consensus immutable) |
| `stamp()` writes a `MOCK_OTS_PROOF` string. `verify_proof_format` accepts that prefix and rejects other proofs. | Cannot force coordination (no control over user upgrades) |
| User protection (users control software, exit options available) | Cannot guarantee adoption (code quality ≠ user adoption) |

## Fundamental Principle

The app posts a `governance/merge` status. It does not control repository merge access, and it does not govern the **network commons** (Bitcoin protocol). Users govern the network through voluntary adoption and economic coordination.
