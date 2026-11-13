# Bitcoin Commons Governance System

Central source of truth for governance rules across all Bitcoin Commons repositories (managed by BTCDecoded organization).

## ⚠️ ACTIVATION STATUS

> **For verified system status**: See [SYSTEM_STATUS.md](https://github.com/BTCDecoded/.github/blob/main/SYSTEM_STATUS.md) in the BTCDecoded organization repository.

**Current Status: Phase 1 (Infrastructure Building)**
- ✅ Infrastructure Complete: All core components implemented
- ⚠️ Not Yet Activated: Governance rules are not enforced
- 🔧 Test Keys Only: No real cryptographic enforcement
- 📋 Development Phase: System is in rapid AI-assisted development

**Timeline:** Activation begins as BLVM moves from alpha to beta, on no fixed timeline. Phase 1 is current, and enforcement is not on. Phase 2 waits on community validation and adoption.

## Overview

This repository defines:
1. **Repository Governance** (Binding): Who can merge what, and when
2. **Protocol Governance** (Advisory): User signaling for consensus changes
3. **Emergency Response**: Three-tiered system for critical issues
4. **Maintainer Lifecycle**: Selection, removal, and rotation processes

**Key Distinction:** We govern repository access (binding) and provide guidance for protocol changes (advisory). Users remain sovereign over Bitcoin's consensus rules.

## Constitutional Governance Model

Bitcoin Commons writes a **5-tier constitutional governance system**. Enforcement is off and the keys are test keys. That system operates under the [Bitcoin Commons Compact](COMPACT.md).

### Action Tiers

- **Tier 1: Routine Maintenance** (3-of-5, 7 days) - Bug fixes, documentation, performance
- **Tier 2: Feature Changes** (4-of-5, 30 days) - New RPC methods, P2P changes, wallet features
- **Tier 3: Consensus-Adjacent** (5-of-5, 90 days) - Changes affecting consensus validation
- **Tier 4: Emergency Actions** (4-of-5, 0 days review period) - Pull-request class for critical patches. This is the maintainer pool in `config/action-tiers.yml`, not the keyholder classes.
- **Tier 5: Governance Changes** (two written pairs, neither chosen here: Meta-Governance is 5-of-7 plus 2-of-3 over 90 days; `tier_5_governance` is 5-of-5 over 180 days) - Changes to governance rules themselves

Combined with a repository layer, the longer review wins. An emergency-classed change in blvm-node is 4-of-5 and 60 days. Keyholder activation is `config/emergency-tiers.yml`: the critical class signs 4-of-7 and activates 5-of-7.

### Layer Hierarchy

| Layer | Repository | Signatures | Review Period |
|-------|------------|------------|---------------|
| 1 | [blvm-spec](https://github.com/BTCDecoded/blvm-spec) | 6-of-7 | 180 days (365 for consensus) |
| 2 | [blvm-consensus](https://github.com/BTCDecoded/blvm-consensus) | 6-of-7 | 180 days (365 for consensus) |
| 3 | [blvm-protocol](https://github.com/BTCDecoded/blvm-protocol) | 4-of-5 | 90 days |
| 4 | [blvm-node](https://github.com/BTCDecoded/blvm-node) / [blvm](https://github.com/BTCDecoded/blvm) | 3-of-5 | 60 days |
| 5 | [blvm-sdk](https://github.com/BTCDecoded/blvm-sdk) | 2-of-3 | 14 days |

## Documentation

### Core Documentation
- [docs/ACTION_TIERS.md](docs/ACTION_TIERS.md) - PR action tiers (`action-tiers.yml`) vs emergency tiers
- [COMPACT.md](COMPACT.md) - Bitcoin Commons Compact
- [GOVERNANCE.md](GOVERNANCE.md) - Main governance process
- [LAYER_TIER_MODEL.md](LAYER_TIER_MODEL.md) - How layers and tiers combine
- [SCOPE.md](SCOPE.md) - Repository vs protocol governance

### Guides
- [guides/MAINTAINER_GUIDE.md](guides/MAINTAINER_GUIDE.md) — Maintainer guide
- [guides/ONBOARDING.md](guides/ONBOARDING.md) — New maintainer onboarding
- [REVIEW_EXPECTATIONS.md](REVIEW_EXPECTATIONS.md) — Human reviewer expectations (guidelines for maintainers)
- [guides/REVIEW_INTELLIGENCE.md](guides/REVIEW_INTELLIGENCE.md) — AI-assisted code review intelligence (operating document; Compact, Orange Paper, differential testing)
- [blvm-commons](https://github.com/BTCDecoded/blvm-commons) - Governance enforcement application
- [blvm-docs](https://github.com/BTCDecoded/blvm-docs) - Unified mdBook site: [docs.btcdecoded.org/blvm](https://docs.btcdecoded.org/blvm/)
- **Audit materials** — see security and disclosure policy in this repo (`SECURITY.md`, `guides/`) and organization-wide [SECURITY.md](https://github.com/BTCDecoded/.github/blob/main/SECURITY.md) where applicable
