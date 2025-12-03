# Auto-Registration Integration Guide

## Overview

Commons Contributors are now automatically registered as economic nodes when their contributions meet qualification thresholds. No manual registration required.

## How It Works

### Automatic Flow

```
1. Contribution Made
   ↓
2. ContributionTracker.record_*() called
   ↓
3. CommonsContributorAutoRegistrar.check_and_register() called
   ↓
4. System checks 90-day rolling window contributions
   ↓
5. If thresholds met → auto-generate proof from tracked data
   ↓
6. Auto-register as Commons Contributor economic node
   ↓
7. Auto-activate if cryptographic proofs verify
```

## Integration Points

### 1. After Recording Contributions

**Merge Mining**:
```rust
use bllvm_commons::economic_nodes::auto_registration::CommonsContributorAutoRegistrar;
use bllvm_commons::economic_nodes::registry::EconomicNodeRegistry;
use std::sync::Arc;

// After recording merge mining contribution
contribution_tracker.record_merge_mining_contribution(
    contributor_id,
    chain_id,
    reward_amount_btc,
    contribution_amount_btc,
    timestamp,
).await?;

// Auto-register if qualified
let registrar = CommonsContributorAutoRegistrar::new(
    pool.clone(),
    Arc::new(registry),
    None, // zap_tracker optional
);
if let Some(node_id) = registrar.check_and_register(contributor_id, "merge_miner").await? {
    info!("Auto-registered merge miner {} as economic node {}", contributor_id, node_id);
}
```

**Fee Forwarding**:
```rust
contribution_tracker.record_fee_forwarding_contribution(
    contributor_id,
    tx_hash,
    amount_btc,
    commons_address,
    block_height,
    timestamp,
).await?;

// Auto-register if qualified
registrar.check_and_register(contributor_id, "fee_forwarder").await?;
```

**Zaps** (already integrated in `ZapTracker`):
```rust
// In zap_tracker.rs, after recording zap:
if let Some(ref sender_pubkey) = zap.sender_pubkey {
    let tracker = ContributionTracker::new(pool.clone());
    tracker.record_zap_contribution(sender_pubkey, amount_btc, timestamp, is_proposal_zap).await?;
    
    // Auto-register if qualified
    registrar.check_and_register(sender_pubkey, "zap_user").await?;
}
```

### 2. Periodic Batch Check (Optional)

For catching edge cases and updates:

```rust
// Run hourly/daily to check all contributors
async fn batch_check_contributors(pool: &SqlitePool, registrar: &CommonsContributorAutoRegistrar) -> Result<()> {
    let contributors = sqlx::query(
        r#"
        SELECT DISTINCT contributor_id, contributor_type
        FROM unified_contributions
        WHERE timestamp >= datetime('now', '-90 days')
        "#
    )
    .fetch_all(pool)
    .await?;
    
    for row in contributors {
        let contributor_id: String = row.get("contributor_id");
        let contributor_type: String = row.get("contributor_type");
        registrar.check_and_register(&contributor_id, &contributor_type).await?;
    }
    
    Ok(())
}
```

## Proof Generation

The system automatically generates proofs from tracked data:

### Merge Mining Proof
- Queries `unified_contributions` for merge mining contributions
- Builds `MergeMiningProof` with block hashes and coinbase signatures
- **TODO**: Query actual block data from merge_mining_contributions table if it exists

### Fee Forwarding Proof
- Queries `fee_forwarding_contributions` table
- Builds `FeeForwardingProof` with transaction hashes and block heights
- Fully implemented

### Zap Proof
- Queries `zap_contributions` table
- Builds `ZapProof` with Nostr event IDs and payment hashes
- Fully implemented

## Public Key Management

The system automatically handles public keys:

- **Zap Users**: Uses Nostr pubkey directly (already have this)
- **Merge Miners**: Uses coinbase signature key (TODO: extract from blocks)
- **Fee Forwarders**: Generates keypair on first registration, stores in `contributor_keys` table

## Database Schema

**New Table**: `contributor_keys`
- Maps `contributor_id` to `public_key` for veto signals
- Created by migration: `006_contributor_keys.sql`

## Status

✅ **Implemented**:
- Auto-registration service
- Proof generation from tracked data
- Threshold checking
- Public key management
- Database migration

⚠️ **TODO**:
- Integrate auto-registration calls into `ContributionTracker` methods
- Extract actual block data for merge mining proofs
- Extract coinbase signatures for merge miners' public keys
- Add periodic batch check job
- Add Nostr profile lookup for zap user names

## Code Locations

- **Auto-Registration**: `blvm-commons/src/economic_nodes/auto_registration.rs`
- **Contribution Tracking**: `blvm-commons/src/governance/contributions.rs`
- **Zap Tracking**: `blvm-commons/src/nostr/zap_tracker.rs`
- **Database Migration**: `blvm-commons/src/database/migrations/006_contributor_keys.sql`

