# Layer + Tier Governance Model

## Overview

BTCDecoded uses a **dual-dimensional governance system** combining:

1. **Layers** (Repository Architecture) - Which repository the change affects
2. **Tiers** (Action Classification) - What type of change is being made

When both apply, the system uses the **"most restrictive wins"** rule to ensure maximum security.

## Layer System (Repository Architecture)

Layers represent the architectural hierarchy of BTCDecoded repositories:

| Layer | Repository | Purpose | Signatures | Review Period |
|-------|------------|---------|------------|---------------|
| 1 | Orange Paper | Constitutional | 6-of-7 | 180 days |
| 2 | Consensus Proof | Constitutional | 6-of-7 | 180 days |
| 3 | Protocol Engine | Implementation | 4-of-5 | 90 days |
| 4 | Reference Node | Application | 3-of-5 | 60 days |
| 5 | Developer SDK | Extension | 2-of-3 | 14 days |

**Note:** For consensus rule changes, Layer 1-2 require 365 days review period.

## Tier System (Action Classification)

Tiers represent the type of change being made, regardless of which repository:

| Tier | Type | Signatures | Review Period | Economic Veto |
|------|------|------------|---------------|---------------|
| 1 | Routine Maintenance | 3-of-5 | 7 days | No |
| 2 | Feature Changes | 4-of-5 | 30 days | No |
| 3 | Consensus-Adjacent | 5-of-5 | 90 days | Yes |
| 4 | Emergency Actions | 4-of-5 | 0 days | No |
| 5 | Governance Changes | 5-of-5 | 180 days | Yes |

## Combination Rules

When both Layer and Tier requirements apply, the system takes the **most restrictive** (highest) requirements:

### Decision Matrix

| Layer | Tier | Final Signatures | Final Review | Source |
|-------|------|------------------|--------------|---------|
| 1 | 1 | 6-of-7 | 180 days | Layer 1 |
| 1 | 2 | 6-of-7 | 180 days | Layer 1 |
| 1 | 3 | 6-of-7 | 180 days | Layer 1 |
| 1 | 4 | 6-of-7 | 180 days | Layer 1 |
| 1 | 5 | 6-of-7 | 180 days | Layer 1 |
| 2 | 1 | 6-of-7 | 180 days | Layer 2 |
| 2 | 2 | 6-of-7 | 180 days | Layer 2 |
| 2 | 3 | 6-of-7 | 180 days | Layer 2 |
| 2 | 4 | 6-of-7 | 180 days | Layer 2 |
| 2 | 5 | 6-of-7 | 180 days | Layer 2 |
| 3 | 1 | 4-of-5 | 90 days | Layer 3 |
| 3 | 2 | 4-of-5 | 90 days | Layer 3 |
| 3 | 3 | 5-of-5 | 90 days | Tier 3 |
| 3 | 4 | 4-of-5 | 90 days | Layer 3 |
| 3 | 5 | 5-of-5 | 180 days | Tier 5 |
| 4 | 1 | 3-of-5 | 60 days | Layer 4 |
| 4 | 2 | 4-of-5 | 60 days | Tier 2 |
| 4 | 3 | 5-of-5 | 90 days | Tier 3 |
| 4 | 4 | 4-of-5 | 60 days | Layer 4 |
| 4 | 5 | 5-of-5 | 180 days | Tier 5 |
| 5 | 1 | 2-of-3 | 14 days | Layer 5 |
| 5 | 2 | 4-of-5 | 30 days | Tier 2 |
| 5 | 3 | 5-of-5 | 90 days | Tier 3 |
| 5 | 4 | 4-of-5 | 14 days | Layer 5 |
| 5 | 5 | 5-of-5 | 180 days | Tier 5 |

## Examples

### Example 1: Bug Fix in Protocol Engine (Layer 3, Tier 1)
- **Layer 3**: 4-of-5 signatures, 90 days
- **Tier 1**: 3-of-5 signatures, 7 days
- **Result**: 4-of-5 signatures, 90 days (Layer 3 wins)

### Example 2: New Feature in Developer SDK (Layer 5, Tier 2)
- **Layer 5**: 2-of-3 signatures, 14 days
- **Tier 2**: 4-of-5 signatures, 30 days
- **Result**: 4-of-5 signatures, 30 days (Tier 2 wins)

### Example 3: Consensus-Adjacent Change in Orange Paper (Layer 1, Tier 3)
- **Layer 1**: 6-of-7 signatures, 180 days
- **Tier 3**: 5-of-5 signatures, 90 days
- **Result**: 6-of-7 signatures, 180 days (Layer 1 wins)

### Example 4: Emergency Fix in Reference Node (Layer 4, Tier 4)
- **Layer 4**: 3-of-5 signatures, 60 days
- **Tier 4**: 4-of-5 signatures, 0 days
- **Result**: 4-of-5 signatures, 0 days (Tier 4 wins)

## Economic Veto Requirements

Economic node vetoes are required when:
- **Tier 3+** (Consensus-Adjacent, Emergency, Governance Changes)
- **Any layer** - veto requirements are tier-based, not layer-based

## Emergency Mode Override

When emergency mode is activated:
- All review periods become 30 days maximum
- Signature requirements remain the same
- Economic veto requirements remain the same

## Implementation

The `ThresholdValidator::get_combined_requirements()` method implements this logic:

```rust
pub fn get_combined_requirements(layer: i32, tier: u32) -> (usize, usize, i64) {
    let (layer_sigs_req, layer_sigs_total) = Self::get_threshold_for_layer(layer);
    let layer_review = Self::get_review_period_for_layer(layer, false);
    
    let (tier_sigs_req, tier_sigs_total) = Self::get_tier_threshold(tier);
    let tier_review = Self::get_tier_review_period(tier);
    
    // Take most restrictive (higher requirements)
    let sigs_req = layer_sigs_req.max(tier_sigs_req);
    let sigs_total = layer_sigs_total.max(tier_sigs_total);
    let review = layer_review.max(tier_review);
    
    (sigs_req, sigs_total, review)
}
```

## Configuration Files

This model is configured through:

- `governance/config/repository-layers.yml` - Layer definitions
- `governance/config/action-tiers.yml` - Tier definitions
- `governance/config/tier-classification-rules.yml` - How to classify PRs

## Related Documentation

- [GOVERNANCE.md](GOVERNANCE.md) - Main governance process
- [SCOPE.md](SCOPE.md) - Repository vs protocol governance
- [Configuration Files](config/README.md) - Technical configuration