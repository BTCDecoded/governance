# BTCDecoded Governance Configuration

Central source of truth for governance rules across all BTCDecoded repositories.

## Overview

This repository defines:

1. **Repository Governance** (Binding): Who can merge what, and when
2. **Protocol Governance** (Advisory): User signaling for consensus changes
3. **Emergency Response**: Three-tiered system for critical issues
4. **Maintainer Lifecycle**: Selection, removal, and rotation processes

**Key Distinction:** We govern repository access (binding) and provide guidance for protocol changes (advisory). Users remain sovereign over Bitcoin's consensus rules.

## Layer Hierarchy

1. **Orange Paper** (Layer 1) - Constitutional, 6-of-7, 180 days (365 for consensus)
2. **Consensus Proof** (Layer 2) - Constitutional, 6-of-7, 180 days (365 for consensus)
3. **Protocol Engine** (Layer 3) - Implementation, 4-of-5, 90 days
4. **Reference Node** (Layer 4) - Application, 3-of-5, 60 days
5. **Developer SDK** (Layer 5) - Extension, 2-of-3, 14 days

## Emergency Tier System

Three-tiered response for critical issues:

- **Tier 1 (Critical)**: 0 day review, 4-of-7 signatures, 7 day max (inflation bugs, consensus forks)
- **Tier 2 (Urgent)**: 7 day review, 5-of-7 signatures, 30 day max (security issues, privacy leaks)
- **Tier 3 (Elevated)**: 30 day review, 6-of-7 signatures, 90 day max (important priorities)

All tiers require 5-of-7 emergency keyholders to activate. See `emergency-tiers.yml` for full specification.

## Consensus Change Process

Consensus rule changes have special requirements:

**Repository Approval (Binding):**
- 6-of-7 maintainer signatures
- 365-day review period (1 year)
- BIP specification required
- Security audit required
- Equivalence proof required

**User Activation (Advisory):**
- Optional upgrade released
- Users choose whether to adopt
- Network signaling measured (75% nodes, 90% hashpower recommended)
- No forced adoption—users govern Bitcoin

See `SCOPE.md` for detailed explanation of repository vs. protocol governance.

## Repository Structure

- `repos/` - Per-repository governance rules (including consensus change detection)
- `maintainers/` - Maintainer public keys by layer
- `emergency-tiers.yml` - Emergency response configuration
- `cross-layer-rules.yml` - Cross-repository validation rules
- `warnings/` - Formal warnings (if needed)
- `examples/` - Workflow guides and historical case studies
- `GOVERNANCE.md` - Detailed process documentation
- `SCOPE.md` - Repository vs. protocol governance clarification

## Quick Links

- **[Full Governance Process](GOVERNANCE.md)** - Detailed documentation
- **[Scope Clarification](SCOPE.md)** - What we control vs. what users control
- **[Consensus Change Workflow](examples/consensus-change-workflow.md)** - Step-by-step guide for protocol changes
- **[Emergency Response](examples/emergency-response.md)** - How to activate emergency tiers

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



