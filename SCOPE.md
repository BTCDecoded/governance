# Governance Scope

## Overview

BTCDecoded governance operates on two levels: **Repository Governance** (binding) and **Protocol Governance** (advisory).

## Repository Governance (Binding)

| What We Control | What We Don't Control |
|-----------------|----------------------|
| Merge permissions to BTCDecoded repositories | Bitcoin's consensus rules (immutable) |
| Code quality standards and review processes | Network upgrade activation mechanisms |
| Release creation and versioning | User adoption decisions |
| Maintainer selection and removal | Miner signaling and hash power |
| PR review requirements and signature thresholds | Which software users choose to run |
| Review periods and emergency procedures | Node operator configuration choices |
| Technical standards (code style, testing, security) | Economic decisions and market behavior |

## Protocol Governance (Advisory)

| What We Influence | What We Cannot Do |
|-------------------|-------------------|
| Code quality for consensus changes (approve high-quality code) | Force network adoption (no amount of signatures forces upgrades) |
| User education (documentation, upgrade paths, trade-offs) | Prevent users from running alternative software |
| Community coordination (facilitate discussion, technical analysis) | Control economic incentives or market forces |
| | Override user choice (users remain sovereign) |

## Examples

| Scenario | Repository Governance (Can Do) | Protocol Governance (Cannot Do) |
|----------|-------------------------------|--------------------------------|
| Consensus Rule Change | Require 6-of-7 signatures, 365-day review, BIP spec, audit | Force users to upgrade, control activation, prevent forks |
| Emergency Security Fix | Activate emergency tier, 0-day review, 4-of-5 signatures | Force immediate adoption, prevent running vulnerable software |
| New RPC Method | Require 4-of-5 signatures, 30-day review, technical spec | Force users to use it, control integration, prevent alternatives |

**User Process**: Maintainers approve code → Code released as optional upgrade → Users evaluate and choose → Economic coordination determines adoption → Users can fork or reject

## Economic Node Role

| Function | Scope | Impact |
|----------|-------|--------|
| Veto Power | Tier 3+ changes (consensus-adjacent, emergency, governance) | Binding authority over repository merges |
| Thresholds | 30%+ hashpower AND 40%+ economic activity (Tier 3) | Blocks PR merge |
| Advisory Input | Signal preferences, provide economic analysis | Influences but doesn't force adoption |

**Important**: Economic node vetoes affect repository access, not user choice. Users remain free to run any software.

## Fork Capability

Users can:
- **Repository Fork**: Fork BTCDecoded repositories, maintain own governance rules
- **Protocol Fork**: Create alternative implementations, maintain different consensus rules
- **Exit Strategy**: Always retain option to exit, no single point of failure

## Safeguards and Limitations

| Safeguards | Limitations |
|------------|-------------|
| Multi-signature requirements (no single maintainer control) | Cannot override Bitcoin's design (consensus immutable) |
| Transparency (public decisions, cryptographic audit trail) | Cannot force coordination (no control over user upgrades) |
| User protection (users control software, exit options available) | Cannot guarantee adoption (code quality ≠ user adoption) |

## Fundamental Principle

We govern the **codebase commons** (repository access), not the **network commons** (Bitcoin protocol). Users govern the network through voluntary adoption and economic coordination.
