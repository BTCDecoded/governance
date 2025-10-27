# Cross-Layer Dependencies Architecture

## Overview

The BTCDecoded governance system uses a layered architecture where different layers have different responsibilities and requirements. This document details how layers interact, what dependencies exist between them, and how cross-layer changes are managed.

## Layer Hierarchy

### Layer 1: Orange Paper (Constitutional)
- **Purpose**: Fundamental Bitcoin principles and constitutional rules
- **Authority**: 6-of-7 maintainers, 180 days (365 for consensus changes)
- **Scope**: Core Bitcoin protocol principles, consensus rules
- **Dependencies**: None (foundational layer)

### Layer 2: Consensus Proof (Constitutional)
- **Purpose**: Mathematical proofs and consensus validation
- **Authority**: 6-of-7 maintainers, 180 days (365 for consensus changes)
- **Scope**: Consensus validation, mathematical proofs
- **Dependencies**: Layer 1 (Orange Paper principles)

### Layer 3: Protocol Engine (Implementation)
- **Purpose**: Bitcoin protocol implementation
- **Authority**: 4-of-5 maintainers, 90 days
- **Scope**: P2P protocol, consensus validation implementation
- **Dependencies**: Layer 1, Layer 2

### Layer 4: Reference Node (Application)
- **Purpose**: Complete Bitcoin node implementation
- **Authority**: 3-of-5 maintainers, 60 days
- **Scope**: Full node functionality, RPC interface, wallet
- **Dependencies**: Layer 1, Layer 2, Layer 3

### Layer 5: Developer SDK (Extension)
- **Purpose**: Developer tools and libraries
- **Authority**: 2-of-3 maintainers, 14 days
- **Scope**: Cryptographic primitives, developer tools
- **Dependencies**: Layer 1, Layer 2, Layer 3, Layer 4

## Dependency Rules

### Upward Dependencies

**Rule**: Higher layers can depend on lower layers, but not vice versa.

- **Layer 5** can depend on Layers 1-4
- **Layer 4** can depend on Layers 1-3
- **Layer 3** can depend on Layers 1-2
- **Layer 2** can depend on Layer 1
- **Layer 1** has no dependencies

### Downward Dependencies

**Rule**: Lower layers cannot depend on higher layers.

- **Layer 1** cannot depend on Layers 2-5
- **Layer 2** cannot depend on Layers 3-5
- **Layer 3** cannot depend on Layers 4-5
- **Layer 4** cannot depend on Layer 5

### Circular Dependencies

**Rule**: No circular dependencies are allowed between any layers.

## Cross-Layer Change Process

### Impact Analysis

Before making changes, analyze:
1. **Direct Dependencies**: Which layers directly depend on this layer
2. **Transitive Dependencies**: Which layers indirectly depend on this layer
3. **Breaking Changes**: Whether changes break dependent layers
4. **Migration Path**: How dependent layers will migrate to changes

### Change Coordination

1. **Notification**: Notify all dependent layers of proposed changes
2. **Impact Assessment**: Dependent layers assess impact
3. **Migration Planning**: Plan migration for dependent layers
4. **Staged Rollout**: Implement changes in dependency order
5. **Verification**: Verify all dependent layers work correctly

### Rollback Procedures

1. **Dependency Check**: Identify all dependent layers
2. **Rollback Order**: Roll back in reverse dependency order
3. **Verification**: Verify each layer after rollback
4. **Communication**: Notify all affected layers

## Layer Interaction Examples

### Example 1: Consensus Rule Change

**Scenario**: Adding new consensus rule to Layer 1 (Orange Paper)

**Impact Analysis**:
- **Layer 2**: Must update consensus validation logic
- **Layer 3**: Must implement new consensus rule
- **Layer 4**: Must update node behavior
- **Layer 5**: Must update developer tools

**Change Process**:
1. **Layer 1**: Add consensus rule (6-of-7, 180 days)
2. **Layer 2**: Update validation logic (6-of-7, 180 days)
3. **Layer 3**: Implement consensus rule (4-of-5, 90 days)
4. **Layer 4**: Update node behavior (3-of-5, 60 days)
5. **Layer 5**: Update developer tools (2-of-3, 14 days)

### Example 2: API Change in Layer 4

**Scenario**: Adding new RPC method to Layer 4 (Reference Node)

**Impact Analysis**:
- **Layer 5**: Must update developer tools to use new API
- **Layers 1-3**: No impact (upward dependency)

**Change Process**:
1. **Layer 4**: Add RPC method (3-of-5, 60 days)
2. **Layer 5**: Update developer tools (2-of-3, 14 days)

### Example 3: Breaking Change in Layer 3

**Scenario**: Removing deprecated P2P message type

**Impact Analysis**:
- **Layer 4**: Must update to use new message types
- **Layer 5**: Must update developer tools
- **Layers 1-2**: No impact (upward dependency)

**Change Process**:
1. **Layer 3**: Remove deprecated message (4-of-5, 90 days)
2. **Layer 4**: Update message handling (3-of-5, 60 days)
3. **Layer 5**: Update developer tools (2-of-3, 14 days)

## Dependency Validation

### Automated Validation

The governance-app validates dependencies by:
1. **Dependency Graph**: Building dependency graph from layer definitions
2. **Circular Check**: Detecting circular dependencies
3. **Impact Analysis**: Analyzing impact of proposed changes
4. **Migration Planning**: Suggesting migration paths

### Manual Validation

Maintainers validate dependencies by:
1. **Code Review**: Reviewing code for dependencies
2. **Impact Assessment**: Assessing impact on dependent layers
3. **Testing**: Testing changes with dependent layers
4. **Documentation**: Documenting dependency changes

## Conflict Resolution

### Dependency Conflicts

When conflicts arise:
1. **Conflict Identification**: Identify conflicting dependencies
2. **Impact Assessment**: Assess impact of each option
3. **Stakeholder Input**: Get input from affected layers
4. **Resolution Planning**: Plan resolution strategy
5. **Implementation**: Implement resolution

### Breaking Changes

For breaking changes:
1. **Deprecation Notice**: Give advance notice of breaking changes
2. **Migration Support**: Provide migration tools and documentation
3. **Grace Period**: Allow time for dependent layers to migrate
4. **Verification**: Verify migration before removing old code

## Monitoring and Compliance

### Dependency Monitoring

Monitor dependencies through:
- **Dependency Graph**: Visual representation of dependencies
- **Change Impact**: Impact of changes on dependencies
- **Migration Status**: Status of dependent layer migrations
- **Conflict Detection**: Automated detection of conflicts

### Compliance Enforcement

Enforce compliance through:
- **Automated Checks**: Regular automated dependency checks
- **Manual Audits**: Periodic manual dependency audits
- **Change Reviews**: Review all changes for dependency impact
- **Penalty System**: Consequences for dependency violations

## Best Practices

### Layer Design

1. **Clear Boundaries**: Define clear boundaries between layers
2. **Minimal Dependencies**: Minimize dependencies between layers
3. **Stable Interfaces**: Maintain stable interfaces between layers
4. **Documentation**: Document all dependencies clearly

### Change Management

1. **Impact Analysis**: Always analyze impact before changes
2. **Coordination**: Coordinate changes across layers
3. **Testing**: Test changes with dependent layers
4. **Rollback Planning**: Plan rollback procedures

### Communication

1. **Early Notification**: Notify dependent layers early
2. **Clear Documentation**: Document all changes clearly
3. **Migration Guides**: Provide migration guides
4. **Support**: Provide support during migrations

## Future Enhancements

### Advanced Features

- **Automated Migration**: Automatic migration of dependent layers
- **Dependency Visualization**: Interactive dependency visualization
- **Impact Prediction**: AI-powered impact prediction
- **Conflict Resolution**: Automated conflict resolution

### Integration Improvements

- **API Integration**: Better API integration between layers
- **Real-time Updates**: Real-time dependency updates
- **Mobile Apps**: Mobile interfaces for dependency management
- **Analytics**: Comprehensive dependency analytics

## Formal Verification Separation Rules

### Layer 2 Protection (Consensus-Proof)

**Rule 1: Verification Prerequisite**
- All PRs to consensus-proof MUST pass Kani + proptest verification
- CI status check "Verify Consensus" must show green
- No maintainer signatures allowed until verification passes
- This creates an objective, non-negotiable technical barrier

**Rule 2: No Import Without Verification**
- Layer 3+ (protocol-engine, reference-node, etc.) may only import from Layer 2 if:
  - Target code has passing verification
  - Import is documented in cross-layer manifest
  - Architectural review confirms separation preserved
- Unverified Layer 2 code cannot be imported by higher layers

**Rule 3: Governance Cannot Override**
- Governance layer (Layer 6) cannot:
  - Disable verification requirements for Layer 2
  - Bypass verification checks
  - Modify verification tools without meta-governance
- Ostrom Principle #1: Clearly Defined Boundaries
- Technical correctness is non-negotiable

**Rule 4: Verification Changes Require Meta-Governance**
- Changes to verification requirements (tools, thresholds, CI) require:
  - 5-of-7 maintainer signatures
  - 90-day review period
  - Public comment period
  - Rationale document
- Ostrom Principle #3: Collective Choice
- Community can propose verification improvements

**Rule 5: Cross-Layer Verification Enforcement**
- Layer 3+ changes that affect Layer 2 verification must:
  - Pass their own verification (if applicable)
  - Not break Layer 2 verification
  - Maintain verification coverage
- Breaking Layer 2 verification blocks all dependent layers

### Defense Against Capture

Formal verification makes Bitcoin governance **6x harder to capture**:

1. **Technical Barrier**: Must bypass automated verification
2. **Social Barrier**: Must convince 6-of-7 maintainers
3. **Time Barrier**: 180-365 day review periods
4. **Transparency Barrier**: All verification results public
5. **Audit Barrier**: OpenTimestamps immutable proof
6. **Community Barrier**: Public review + economic node veto

**Key Insight**: An attacker cannot simply "convince maintainers" - they must also produce mathematically correct code that passes verification. This dramatically raises the bar for malicious changes.

### Verification Integration Examples

#### Example 1: Consensus Rule Change with Verification

**Scenario**: Adding new consensus rule to Layer 1 (Orange Paper)

**Impact Analysis**:
- **Layer 2**: Must update consensus validation logic + pass verification
- **Layer 3**: Must implement new consensus rule (may need verification)
- **Layer 4**: Must update node behavior
- **Layer 5**: Must update developer tools

**Change Process**:
1. **Layer 1**: Add consensus rule (6-of-7, 180 days)
2. **Layer 2**: Update validation logic + pass Kani/proptest (6-of-7, 180 days)
3. **Layer 3**: Implement consensus rule (4-of-5, 90 days)
4. **Layer 4**: Update node behavior (3-of-5, 60 days)
5. **Layer 5**: Update developer tools (2-of-3, 14 days)

**Verification Requirements**:
- Layer 2 changes MUST pass verification before Layer 3 can proceed
- Layer 3 changes cannot break Layer 2 verification
- All verification results are timestamped and immutable

#### Example 2: Verification Tool Update

**Scenario**: Updating Kani version in Layer 2

**Impact Analysis**:
- **Layer 2**: Must update verification tools + pass new verification
- **Layer 3+**: May need to update if verification requirements change

**Change Process**:
1. **Meta-Governance**: 5-of-7 maintainers approve tool update (90 days)
2. **Layer 2**: Update verification tools + pass verification
3. **Layer 3+**: Update if affected by new verification requirements

**Verification Requirements**:
- Tool updates require meta-governance approval
- All existing verification must continue to pass
- New verification requirements must be documented

### Verification Monitoring

#### Automated Monitoring

- **CI Status**: Monitor verification CI status for all Layer 2 PRs
- **Coverage Tracking**: Track verification coverage across Layer 2
- **Tool Status**: Monitor verification tool health and performance
- **Dependency Impact**: Monitor impact of changes on verification

#### Manual Audits

- **Verification Review**: Periodic review of verification quality
- **Tool Assessment**: Assessment of verification tool effectiveness
- **Coverage Analysis**: Analysis of verification coverage gaps
- **Process Improvement**: Continuous improvement of verification process

## References

- [Repository Layers Configuration](../config/repository-layers.yml)
- [Action Tiers Configuration](../config/action-tiers.yml)
- [Cross-Layer Rules](../config/cross-layer-rules.yml)
- [Maintainer Guide](../guides/MAINTAINER_GUIDE.md)
- [Consensus Proof Verification](../consensus-proof/docs/VERIFICATION.md)
