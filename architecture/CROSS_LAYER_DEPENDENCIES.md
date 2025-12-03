# Cross-Layer Dependencies

## Overview

Layered architecture where different layers have different responsibilities. Higher layers can depend on lower layers, but not vice versa. No circular dependencies allowed.

## Layer Hierarchy

| Layer | Repository | Purpose | Authority | Dependencies |
|-------|------------|---------|-----------|--------------|
| 1 | blvm-spec | Fundamental Bitcoin principles | 6-of-7, 180d (365d consensus) | None (foundational) |
| 2 | blvm-consensus | Mathematical proofs and consensus validation | 6-of-7, 180d (365d consensus) | Layer 1 |
| 3 | blvm-protocol | Bitcoin protocol implementation | 4-of-5, 90d | Layers 1-2 |
| 4 | blvm-node / bllvm | Complete Bitcoin node implementation | 3-of-5, 60d | Layers 1-3 |
| 5 | blvm-sdk | Developer tools and libraries | 2-of-3, 14d | Layers 1-4 |

## Dependency Rules

| Rule | Description |
|------|-------------|
| **Upward Dependencies** | Higher layers can depend on lower layers (Layer 5 → 1-4, Layer 4 → 1-3, etc.) |
| **Downward Dependencies** | Lower layers cannot depend on higher layers (Layer 1 cannot depend on 2-5) |
| **Circular Dependencies** | No circular dependencies allowed between any layers |

## Cross-Layer Change Process

### Impact Analysis

Before making changes, analyze: direct dependencies, transitive dependencies, breaking changes, migration path.

### Change Coordination

1. Notification (notify all dependent layers)
2. Impact assessment (dependent layers assess impact)
3. Migration planning (plan migration for dependent layers)
4. Staged rollout (implement in dependency order)
5. Verification (verify all dependent layers work correctly)

### Rollback Procedures

1. Dependency check (identify all dependent layers)
2. Rollback order (roll back in reverse dependency order)
3. Verification (verify each layer after rollback)
4. Communication (notify all affected layers)

## Examples

| Scenario | Impact | Change Process |
|----------|--------|----------------|
| Consensus rule change in blvm-spec | Layers 2-5 must update | Layer 1 (6-of-7, 180d) → Layer 2 (6-of-7, 180d) → Layer 3 (4-of-5, 90d) → Layer 4 (3-of-5, 60d) → Layer 5 (2-of-3, 14d) |
| New RPC method in blvm-node | Layer 5 must update | Layer 4 (3-of-5, 60d) → Layer 5 (2-of-3, 14d) |
| Breaking change in blvm-protocol | Layers 4-5 must update | Layer 3 (4-of-5, 90d) → Layer 4 (3-of-5, 60d) → Layer 5 (2-of-3, 14d) |

## Dependency Validation

### Automated Validation

Governance-app validates by: building dependency graph, detecting circular dependencies, analyzing impact of proposed changes, suggesting migration paths.

### Manual Validation

Maintainers validate by: reviewing code for dependencies, assessing impact on dependent layers, testing changes with dependent layers, documenting dependency changes.

**Code**: ```blvm-commons/src/validation/cross_layer.rs```
