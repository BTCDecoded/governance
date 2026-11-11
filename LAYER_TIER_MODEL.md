# Layer + Tier Governance Model

## Overview

Dual-dimensional governance combining **Layers** (repository architecture) and **Tiers** (action classification). When both apply, **most restrictive wins**.

## Layer System

| Layer | Repository | Purpose | Signatures | Review Period |
|-------|------------|---------|------------|---------------|
| 1 | blvm-spec | Constitutional | 6-of-7 | 180 days |
| 2 | blvm-consensus, blvm-primitives, blvm-secp256k1 | Constitutional | 6-of-7 | 180 days |
| 3 | blvm-protocol | Implementation | 4-of-5 | 90 days |
| 4 | blvm-node / blvm | Application | 3-of-5 | 60 days |
| 5 | blvm-sdk | Extension | 2-of-3 | 14 days |

**Note:** For consensus rule changes, Layer 1-2 require 365 days review period.

A shipped policy default, including relay policy and spam-filter parameters, stays on the tier and layer it already has. It is not reclassified as Tier 3. The change carries a written rationale tied to the Compact and a statement of whether that purpose is contested. No signature count and no review period in this table changes.

Paths in `blvm-node` that build the state consensus is given are consensus-adjacent, not ordinary node code. The class is the UTXO store (`src/storage/utxostore.rs`, `src/storage/disk_utxo.rs`, `src/storage/ibd_utxo_store.rs`), reorg handling (`src/node/reorg_executor.rs` and undo data in `src/storage/blockstore.rs`), and block connection (`src/node/sync.rs`). They use the consensus-adjacent tier already written. Ordinary node changes stay on layer 4. No signature count and no review period changes. Consensus is pure, so it is only as correct as those inputs. A change above that class mostly risks liveness rather than a split. `blvm-primitives` and `blvm-secp256k1` are named on layer 2 with `blvm-consensus`. That classification does not change a signature count or a review period.

## Tier System

| Tier | Type | Signatures | Review Period |
|------|------|------------|---------------|
| 1 | Routine Maintenance | 3-of-5 | 7 days |
| 2 | Feature Changes | 4-of-5 | 30 days |
| 3 | Consensus-Adjacent | 5-of-5 | 90 days |
| 4 | Emergency Actions | 4-of-5 | 0 days |
| 5 | Governance Changes | 5-of-5 | 180 days |

## Combination Rules

When both apply, system takes **most restrictive** (highest) requirements:

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
| 4 | 2 | 4-of-5 | 60 days | Tier 2 signatures, Layer 4 review |
| 4 | 3 | 5-of-5 | 90 days | Tier 3 |
| 4 | 4 | 4-of-5 | 60 days | Tier 4 signatures, Layer 4 review |
| 4 | 5 | 5-of-5 | 180 days | Tier 5 |
| 5 | 1 | 2-of-3 | 14 days | Layer 5 |
| 5 | 2 | 4-of-5 | 30 days | Tier 2 |
| 5 | 3 | 5-of-5 | 90 days | Tier 3 |
| 5 | 4 | 4-of-5 | 14 days | Tier 4 signatures, Layer 5 review |
| 5 | 5 | 5-of-5 | 180 days | Tier 5 |

Rows for layers 1 and 2 use the ordinary `review_period_days` of 180 days. A consensus rule change on those layers uses 365 days. Tier 3 is not only consensus-rule changes. The layer-1 tier-3 cell stays 180 days.

## Examples

| Example | Layer | Tier | Result | Source |
|---------|-------|------|--------|--------|
| Bug fix in blvm-protocol | 3 (4-of-5, 90d) | 1 (3-of-5, 7d) | 4-of-5, 90d | Layer 3 |
| New feature in blvm-sdk | 5 (2-of-3, 14d) | 2 (4-of-5, 30d) | 4-of-5, 30d | Tier 2 |
| Consensus change in blvm-spec | 1 (6-of-7, 180d) | 3 (5-of-5, 90d) | 6-of-7, 180 days (consensus rule change: 365) | Layer 1 |
| Emergency fix in blvm-node | 4 (3-of-5, 60d) | 4 (4-of-5, 0d) | 4-of-5, 60d | Combined Layer 4 + Tier 4 |

## Implementation

**Code**: ```63:125:blvm-commons/src/validation/threshold.rs```

```rust
pub fn get_combined_requirements(layer: i32, tier: u32) -> (usize, usize, i64) {
    let (layer_sigs_req, layer_sigs_total) = Self::get_threshold_for_layer(layer);
    let layer_review = Self::get_review_period_for_layer(layer, false);
    let (tier_sigs_req, tier_sigs_total) = Self::get_tier_threshold(tier);
    let tier_review = Self::get_tier_review_period(tier);
    // Take most restrictive
    (layer_sigs_req.max(tier_sigs_req), layer_sigs_total.max(tier_sigs_total), layer_review.max(tier_review))
}
```

**Test**: `cd blvm-commons && cargo test threshold`

## Configuration

- `config/repository-layers.yml` - Layer definitions
- `config/action-tiers.yml` - Tier definitions
- `config/tier-classification-rules.yml` - PR classification