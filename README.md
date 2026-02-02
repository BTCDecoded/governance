# Bitcoin Commons Governance System

Central source of truth for governance rules across all Bitcoin Commons repositories (managed by BTCDecoded organization).

## ⚠️ ACTIVATION STATUS

> **For verified system status**: See [SYSTEM_STATUS.md](https://github.com/BTCDecoded/.github/blob/main/SYSTEM_STATUS.md) in the BTCDecoded organization repository.

**Current Status: Phase 1 (Infrastructure Building)**
- ✅ Infrastructure Complete: All core components implemented
- ⚠️ Not Yet Activated: Governance rules are not enforced
- 🔧 Test Keys Only: No real cryptographic enforcement
- 📋 Development Phase: System is in rapid AI-assisted development

**Timeline:** Phase 2 Activation: Governance enforcement begins | Phase 3 Full Operation: Mature, stable system

## Overview

This repository defines:
1. **Repository Governance** (Binding): Who can merge what, and when
2. **Protocol Governance** (Advisory): User signaling for consensus changes
3. **Emergency Response**: Three-tiered system for critical issues
4. **Maintainer Lifecycle**: Selection, removal, and rotation processes

**Key Distinction:** We govern repository access (binding) and provide guidance for protocol changes (advisory). Users remain sovereign over Bitcoin's consensus rules.

## Constitutional Governance Model

Bitcoin Commons implements a **5-tier constitutional governance system** with complete transparency through cryptographic audit trails and user-protective mechanisms.

### Action Tiers

- **Tier 1: Routine Maintenance** (3-of-5, 7 days) - Bug fixes, documentation, performance
- **Tier 2: Feature Changes** (4-of-5, 30 days) - New RPC methods, P2P changes, wallet features
- **Tier 3: Consensus-Adjacent** (5-of-5, 90 days) - Changes affecting consensus validation
- **Tier 4: Emergency Actions** (4-of-5, 0 days review period) - Critical security patches, network threats
- **Tier 5: Governance Changes** (Special process, 180 days) - Changes to governance rules themselves

### Layer Hierarchy

| Layer | Repository | Signatures | Review Period |
|-------|------------|------------|---------------|
| 1 | [blvm-spec](../blvm-spec/README.md) | 6-of-7 | 180 days (365 for consensus) |
| 2 | [blvm-consensus](../blvm-consensus/README.md) | 6-of-7 | 180 days (365 for consensus) |
| 3 | [blvm-protocol](../blvm-protocol/README.md) | 4-of-5 | 90 days |
| 4 | [blvm-node](../blvm-node/README.md) / [blvm](../blvm/README.md) | 3-of-5 | 60 days |
| 5 | [blvm-sdk](../blvm-sdk/README.md) | 2-of-3 | 14 days |

## Documentation

### Quick Reference
- [GETTING_STARTED.md](GETTING_STARTED.md) - Quick orientation
- [QUICK_REFERENCE.md](QUICK_REFERENCE.md) - Lookup tables and commands
- [HOW_TO.md](HOW_TO.md) - Task instructions
- [DECISION_TREES.md](DECISION_TREES.md) - Decision flows

### Core Documentation
- [GOVERNANCE.md](GOVERNANCE.md) - Main governance process
- [LAYER_TIER_MODEL.md](LAYER_TIER_MODEL.md) - How layers and tiers combine
- [SCOPE.md](SCOPE.md) - Repository vs protocol governance

### Guides
- [guides/MAINTAINER_GUIDE.md](guides/MAINTAINER_GUIDE.md) - Maintainer guide
- [guides/ECONOMIC_NODE_GUIDE.md](guides/ECONOMIC_NODE_GUIDE.md) - Economic node guide
- [guides/ONBOARDING.md](guides/ONBOARDING.md) - New maintainer onboarding

### Related Repositories
- [blvm-commons](../blvm-commons/README.md) - Governance enforcement application
- [Audit Materials](../audit-materials/README.md) - Security and audit information
