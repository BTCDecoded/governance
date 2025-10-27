# BTCDecoded Governance System

Central source of truth for governance rules across all BTCDecoded repositories.

## ⚠️ ACTIVATION STATUS

**Current Status: Phase 1 (Infrastructure Building)**

- ✅ **Infrastructure Complete**: All core components implemented
- ⚠️ **Not Yet Activated**: Governance rules are not enforced
- 🔧 **Test Keys Only**: No real cryptographic enforcement
- 📋 **Development Phase**: System is in rapid AI-assisted development

**Timeline:**
- **Phase 2 Activation**: 3-6 months (governance enforcement begins)
- **Phase 3 Full Operation**: 12+ months (mature, stable system)

## Overview

This repository defines:

1. **Repository Governance** (Binding): Who can merge what, and when
2. **Protocol Governance** (Advisory): User signaling for consensus changes
3. **Emergency Response**: Three-tiered system for critical issues
4. **Maintainer Lifecycle**: Selection, removal, and rotation processes

**Key Distinction:** We govern repository access (binding) and provide guidance for protocol changes (advisory). Users remain sovereign over Bitcoin's consensus rules.

## Constitutional Governance Model

BTCDecoded implements a **5-tier constitutional governance system** that makes Bitcoin governance **6x harder to capture** than Bitcoin Core's current model, with **complete transparency** through cryptographic audit trails and **user-protective** mechanisms.

### Action Tiers

- **Tier 1: Routine Maintenance** (3-of-5, 7 days) - Bug fixes, documentation, performance
- **Tier 2: Feature Changes** (4-of-5, 30 days) - New RPC methods, P2P changes, wallet features
- **Tier 3: Consensus-Adjacent** (5-of-5, 90 days + economic node veto) - Changes affecting consensus validation
- **Tier 4: Emergency Actions** (4-of-5, 0 days review period) - Critical security patches, network threats
- **Tier 5: Governance Changes** (Special process, 180 days) - Changes to governance rules themselves

### Layer Hierarchy

1. **Orange Paper** (Layer 1) - Constitutional, 6-of-7, 180 days (365 for consensus)
2. **Consensus Proof** (Layer 2) - Constitutional, 6-of-7, 180 days (365 for consensus)
3. **Protocol Engine** (Layer 3) - Implementation, 4-of-5, 90 days
4. **Reference Node** (Layer 4) - Application, 3-of-5, 60 days
5. **Developer SDK** (Layer 5) - Extension, 2-of-3, 14 days

## Directory Structure

```
governance/
├── README.md (this file - navigation hub)
├── GOVERNANCE.md (core governance process)
├── LAYER_TIER_MODEL.md (how layers and tiers combine)
├── SCOPE.md (repository vs protocol governance)
├── LICENSE
│
├── guides/ (comprehensive guides)
│   ├── MAINTAINER_GUIDE.md
│   └── ECONOMIC_NODE_GUIDE.md
│
├── activation/ (activation process)
│   ├── PHASE_ACTIVATION.md
│   └── ACTIVATION_CHECKLIST.md (coming soon)
│
├── config/ (configuration files)
│   ├── action-tiers.yml (tier definitions)
│   ├── repository-layers.yml (layer definitions)
│   ├── tier-classification-rules.yml (PR classification)
│   ├── economic-nodes.yml
│   ├── emergency-tiers.yml
│   ├── governance-fork.yml
│   ├── ruleset-export-template.yml
│   ├── maintainers/ (by layer)
│   └── repos/ (by repository)
│
├── examples/ (workflow examples)
│   ├── consensus-change-workflow.md
│   ├── emergency-response.md
│   ├── tier1-routine-pr.md (coming soon)
│   ├── tier3-consensus-adjacent.md (coming soon)
│   └── economic-node-veto.md (coming soon)
│
└── architecture/ (design documentation)
    ├── CRYPTOGRAPHIC_GOVERNANCE.md
    ├── ECONOMIC_NODES.md
    ├── GOVERNANCE_FORK.md
    └── CROSS_LAYER_DEPENDENCIES.md (coming soon)
```

## Quick Navigation

### For New Users
- [Main Governance Process](GOVERNANCE.md) - How governance works
- [Layer + Tier Model](LAYER_TIER_MODEL.md) - How layers and tiers combine
- [Governance Scope](SCOPE.md) - What we control vs what we influence
- [Maintainer Guide](guides/MAINTAINER_GUIDE.md) - If you're a maintainer
- [Economic Node Guide](guides/ECONOMIC_NODE_GUIDE.md) - If you're an economic node
- [Examples](examples/README.md) - See governance in action

### For Maintainers
- [Maintainer Guide](guides/MAINTAINER_GUIDE.md) - Complete maintainer documentation
- [Configuration Files](config/README.md) - How to modify configuration
- [Activation Process](activation/README.md) - When governance will be activated
- [Examples](examples/README.md) - Practical workflows

### For Economic Nodes
- [Economic Node Guide](guides/ECONOMIC_NODE_GUIDE.md) - Complete economic node documentation
- [Economic Node Configuration](config/economic-nodes.yml) - Configuration details
- [Veto Examples](examples/economic-node-veto.md) - How veto process works
- [Activation Timeline](activation/README.md) - When to expect activation

### For Developers
- [Architecture Documentation](architecture/README.md) - System design
- [Configuration Reference](config/README.md) - Technical configuration
- [Governance App Documentation](../governance-app/README.md) - Implementation details
- [Audit Materials](../audit-materials/README.md) - Security and audit information

### For Auditors
- [Audit Materials](../audit-materials/README.md) - Complete audit documentation
- [Architecture Documentation](architecture/README.md) - System design
- [Security Documentation](../audit-materials/02-security/README.md) - Security details
- [Test Coverage](../audit-materials/03-testing/README.md) - Testing information

## Key Principles

1. **Dual-Track Governance**: Repository (binding) + Protocol (advisory)
2. **User Sovereignty**: No forced network upgrades
3. **Proportional Response**: Emergency tiers match threat severity
4. **Transparency**: All governance events logged and auditable
5. **Ostrom Compliance**: Managing the codebase commons properly

## For Maintainers

Your role:
- Steward the codebase (binding authority)
- Review and approve quality code
- Coordinate releases
- Advocate for good protocol design
- **Serve users, don't command them**

You control: Repository merges, releases, code quality
You don't control: Network adoption, user choices, Bitcoin consensus

## For Users

Your role:
- Choose software that serves your needs
- Signal preferences through adoption
- Participate in protocol discussions
- Fork if dissatisfied
- **Exercise sovereignty responsibly**

You control: What software you run, Bitcoin consensus rules (via economic coordination)
You don't control: What maintainers work on, release timing

## Contributing

To propose governance changes:

1. Open discussion in this repository
2. Build consensus among maintainers and community
3. Submit PR (requires 5-of-7 maintainers + 2-of-3 emergency keyholders)
4. 90-day review + 30-day public comment period

See `GOVERNANCE.md` section on Meta-Governance for details.

## Related Documentation

- [Audit Materials](../audit-materials/README.md) - Security and audit information
- [Governance App](../governance-app/README.md) - Implementation details
- [Developer SDK](../developer-sdk/README.md) - Cryptographic primitives
- [Orange Paper](../orange-paper/README.md) - Constitutional layer
- [Consensus Proof](../consensus-proof/README.md) - Constitutional layer
- [Protocol Engine](../protocol-engine/README.md) - Implementation layer
- [Reference Node](../reference-node/README.md) - Application layer



