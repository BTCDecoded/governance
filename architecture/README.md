# Governance Architecture

This directory contains detailed architectural documentation for the BTCDecoded governance system.

## Available Documents

- **[CRYPTOGRAPHIC_GOVERNANCE.md](./CRYPTOGRAPHIC_GOVERNANCE.md)** - Core cryptographic governance concepts
- **[ECONOMIC_NODES.md](./ECONOMIC_NODES.md)** - Economic node system design
- **[GOVERNANCE_FORK.md](./GOVERNANCE_FORK.md)** - Governance fork mechanism design
- **[CROSS_LAYER_DEPENDENCIES.md](./CROSS_LAYER_DEPENDENCIES.md)** - Cross-layer dependency management (coming soon)

## Architecture Overview

The BTCDecoded governance system implements a **5-tier constitutional governance model** that makes Bitcoin governance **6x harder to capture** than Bitcoin Core's current model.

### Core Principles

1. **Cryptographic Enforcement**: Apply the same cryptographic enforcement to governance that Bitcoin applies to consensus
2. **Transparency**: Complete transparency through cryptographic audit trails
3. **User Protection**: User-protective mechanisms with economic node veto
4. **Consensus Immutability**: Bitcoin's consensus rules are sacred and cannot be altered

### System Components

- **Governance App**: GitHub App for enforcing governance rules
- **Economic Nodes**: Mining pools, exchanges, custodians with veto power
- **Governance Fork**: Mechanism for users to choose between governance rulesets
- **Developer SDK**: Cryptographic primitives for governance
- **Audit System**: Comprehensive logging and monitoring

## Quick Links

- [Main Governance Process](../GOVERNANCE.md)
- [Maintainer Guide](../guides/MAINTAINER_GUIDE.md)
- [Economic Node Guide](../guides/ECONOMIC_NODE_GUIDE.md)
- [Configuration Files](../config/README.md)
- [Examples](../examples/README.md)

## For Developers

- Review [Cryptographic Governance](./CRYPTOGRAPHIC_GOVERNANCE.md) for core concepts
- Review [Economic Nodes](./ECONOMIC_NODES.md) for veto system design
- Review [Governance Fork](./GOVERNANCE_FORK.md) for fork mechanism
- Review [Audit Materials](../../audit-materials/README.md) for security details

## For Architects

- Understand the 5-tier model
- Review cross-layer dependencies
- Understand economic node integration
- Review governance fork design
- Consider security implications

## For Auditors

- Review [Audit Materials](../../audit-materials/README.md)
- Focus on cryptographic design
- Review threat model
- Understand key management
- Review test coverage




