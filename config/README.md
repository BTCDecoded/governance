# Governance Configuration

This directory contains all configuration files for the BTCDecoded governance system.

## Configuration Files

### Core Configuration

- **[action-tiers.yml](./action-tiers.yml)** - Defines the 5-tier governance model
- **[cross-layer-rules.yml](./cross-layer-rules.yml)** - Rules for cross-layer dependencies
- **[economic-nodes.yml](./economic-nodes.yml)** - Economic node configuration
- **[emergency-tiers.yml](./emergency-tiers.yml)** - Emergency action tiers
- **[governance-fork.yml](./governance-fork.yml)** - Governance fork configuration
- **[ruleset-export-template.yml](./ruleset-export-template.yml)** - Template for ruleset exports
- **[test-vectors.yml](./test-vectors.yml)** - Test vectors for equivalence proof validation (Orange Paper ↔ Consensus Proof)

### Maintainer Configuration

- **[maintainers/](./maintainers/)** - Maintainer definitions by layer
  - `layer-1-2.yml` - Constitutional layers (orange-paper, consensus-proof)
  - `layer-3.yml` - Implementation layer (protocol-engine)
  - `layer-4.yml` - Application layer (reference-node)
  - `emergency.yml` - Emergency keyholders

### Repository Configuration

- **[repos/](./repos/)** - Repository-specific configuration
  - `orange-paper.yml` - Layer 1 configuration
  - `consensus-proof.yml` - Layer 2 configuration
  - `protocol-engine.yml` - Layer 3 configuration
  - `reference-node.yml` - Layer 4 configuration
  - `developer-sdk.yml` - Layer 5 configuration

## Governance App Integration

The governance-app loads and uses these configuration files to enforce governance rules. The app automatically loads configuration from this directory and validates it on startup.

### Configuration Loading

The governance-app loads configuration files in the following order:
1. **Default Configuration**: Built-in default values
2. **File Configuration**: Configuration files from this directory
3. **Environment Variables**: Environment variable overrides
4. **Command Line Arguments**: Command line argument overrides

### File Usage

- **action-tiers.yml**: Used for PR tier classification and signature requirements
- **repository-layers.yml**: Used for layer-specific requirements and maintainer counts
- **tier-classification-rules.yml**: Used for automatic PR tier detection
- **economic-nodes.yml**: Used for economic node veto system
- **maintainers/**: Used for maintainer registry and signature verification
- **repos/**: Used for repository-specific governance rules
- **test-vectors.yml**: Used for cross-layer equivalence proof validation (Phase 1: optional with fallback, Phase 2: required)

### Configuration Validation

The governance-app validates all configuration files on startup:
- YAML syntax validation
- Required field validation
- Type checking
- Cross-reference validation
- Signature requirement validation
- Layer/tier consistency validation

### Error Handling

If configuration files are invalid or missing:
- The app will log detailed error messages
- Fallback to default configuration if possible
- Fail to start if critical configuration is missing
- Provide clear error messages for fixing issues

## Configuration Management

### Modifying Configuration

1. **Never edit production configs directly**
2. **Create a PR with your changes**
3. **Follow the governance process** (see [GOVERNANCE.md](../GOVERNANCE.md))
4. **Test changes in development first**
5. **Verify governance-app can load the configuration**

### Validation

All configuration files are validated against schemas:
- YAML syntax validation
- Required field validation
- Type checking
- Cross-reference validation
- Governance-app compatibility validation

### Security

- Configuration files are version controlled
- Changes require maintainer signatures
- Sensitive data (keys, tokens) stored separately
- Configuration integrity verified on deployment

## Quick Links

- [Main Governance Process](../GOVERNANCE.md)
- [Maintainer Guide](../guides/MAINTAINER_GUIDE.md)
- [Economic Node Guide](../guides/ECONOMIC_NODE_GUIDE.md)
- [Examples](../examples/README.md)

## For Developers

- Configuration files use YAML format
- All files have corresponding schemas
- Changes trigger automatic validation
- Configuration is loaded at startup
- Hot-reloading not supported (restart required)

## For Maintainers

- Review configuration changes carefully
- Ensure all required fields are present
- Verify cross-references are valid
- Test changes in development environment
- Follow governance process for changes




