# Commons Contributor Automatic Registration

## Current State

### What Exists ✅

1. **Automatic Contribution Tracking**:
   - `ContributionTracker` records merge mining, fee forwarding, and zaps in `unified_contributions` table
   - `ZapTracker` automatically subscribes to Nostr zap events and records them
   - Merge mining contributions detected when blocks are mined with Commons fees
   - Fee forwarding contributions detected when transactions forward fees to Commons address

2. **Automatic Registration** (✅ **IMPLEMENTED**):
   - `CommonsContributorAutoRegistrar` automatically checks thresholds when contributions are recorded
   - Auto-generates proofs from tracked contribution data
   - Auto-registers contributors as economic nodes when thresholds met
   - Auto-activates if cryptographic proofs verify

**Code**: ```1:498:blvm-commons/src/economic_nodes/auto_registration.rs```

## Gap Analysis

| Component | Status | Implementation |
|-----------|--------|---------------|
| **Contribution Detection** | ✅ Automatic | Merge mining, fee forwarding, zaps all tracked automatically |
| **Threshold Checking** | ✅ Automatic | `CommonsContributorAutoRegistrar.check_and_register()` checks on contribution |
| **Proof Generation** | ✅ Automatic | `generate_proof_from_contributions()` builds proof from tracked data |
| **Registration** | ✅ Automatic | `check_and_register()` calls `register_economic_node()` automatically |

## Proposed Solution: Automatic Registration

### Architecture

```
Contribution Detected
    ↓
Recorded in unified_contributions
    ↓
Periodic Check (or event-driven)
    ↓
Aggregate contributions (90-day rolling window)
    ↓
Check if thresholds met
    ↓
Auto-generate proof from tracked data
    ↓
Verify cryptographic proofs
    ↓
Auto-register as Commons Contributor economic node
```

### Implementation Plan

#### 1. Add Automatic Registration Service

**File**: `blvm-commons/src/economic_nodes/auto_registration.rs`

```rust
pub struct CommonsContributorAutoRegistrar {
    pool: SqlitePool,
    registry: Arc<EconomicNodeRegistry>,
    contribution_tracker: ContributionTracker,
}

impl CommonsContributorAutoRegistrar {
    /// Check if contributor qualifies and auto-register
    pub async fn check_and_register(
        &self,
        contributor_id: &str,
        contributor_type: &str, // "merge_miner", "fee_forwarder", "zap_user"
    ) -> Result<Option<i32>> {
        // 1. Get contributions in 90-day window
        let end_time = Utc::now();
        let start_time = end_time - Duration::days(90);
        let total = self.contribution_tracker
            .get_contributor_total(contributor_id, start_time, end_time)
            .await?;
        
        // 2. Check if already registered
        let existing = self.registry
            .get_node_by_contributor_id(contributor_id)
            .await?;
        if existing.is_some() {
            return Ok(None); // Already registered
        }
        
        // 3. Check thresholds
        let thresholds = self.registry.get_commons_contributor_thresholds().await?;
        let qualified = self.check_qualification(&total, &thresholds).await?;
        
        if !qualified {
            return Ok(None); // Doesn't meet thresholds yet
        }
        
        // 4. Auto-generate proof from tracked contributions
        let proof = self.generate_proof_from_contributions(contributor_id, &total).await?;
        
        // 5. Auto-register
        let node_id = self.registry
            .register_economic_node(
                NodeType::CommonsContributor,
                &self.get_entity_name(contributor_id, contributor_type).await?,
                &self.get_or_generate_public_key(contributor_id).await?,
                &proof,
                Some("auto_registration"),
            )
            .await?;
        
        Ok(Some(node_id))
    }
    
    /// Generate proof from tracked contributions
    async fn generate_proof_from_contributions(
        &self,
        contributor_id: &str,
        total: &ContributorTotal,
    ) -> Result<QualificationProof> {
        // Build proof from unified_contributions data
        // - Merge mining: Get blocks from merge_mining_contributions
        // - Fee forwarding: Get transactions from fee_forwarding_contributions  
        // - Zaps: Get events from zap_contributions
        // - Marketplace: Get payments from marketplace_payments (if exists)
    }
}
```

#### 2. Event-Driven Registration

**Option A: On Contribution Recorded**
- When `ContributionTracker.record_*()` is called, trigger check
- If threshold met → auto-register immediately

**Option B: Periodic Batch Check**
- Cron job runs every hour/day
- Checks all contributors in `unified_contributions`
- Registers any that meet thresholds

**Recommended**: Hybrid approach
- Event-driven for immediate registration when threshold crossed
- Periodic batch for catching edge cases and updates

#### 3. Proof Generation from Tracked Data

**Merge Mining Proof**:
```rust
// Query merge_mining_contributions table
// Build MergeMiningProof with:
// - blocks_mined: from tracked block hashes
// - coinbase_signatures: from tracked signatures
// - total_revenue_btc: sum from unified_contributions
```

**Fee Forwarding Proof**:
```rust
// Query fee_forwarding_contributions table
// Build FeeForwardingProof with:
// - blocks_with_forwarding: from tracked transactions
// - total_fees_forwarded_btc: sum from unified_contributions
```

**Zap Proof**:
```rust
// Query zap_contributions table
// Build ZapProof with:
// - zap_events: from tracked zap events
// - total_zaps_btc: sum from unified_contributions
// - contributor_id: Nostr pubkey (already tracked)
```

#### 4. Public Key Management

**Issue**: Contributors need public key for veto signals, but merge miners/zap users may not have one registered.

**Solution**:
- **Merge Miners**: Use coinbase signature key (already have this)
- **Zap Users**: Use Nostr pubkey (already have this)
- **Fee Forwarders**: Generate keypair on first registration, store in `contributor_keys` table

#### 5. Entity Name Resolution

**Issue**: `contributor_id` is just an ID, need human-readable name.

**Solution**:
- **Merge Miners**: Use chain ID + miner identifier
- **Zap Users**: Query Nostr profile for name, fallback to pubkey prefix
- **Fee Forwarders**: Use address or generated name

## Registration Flow Comparison

### Current (Manual)
```
1. Contributor makes contribution (tracked automatically)
2. Contributor manually queries their contributions
3. Contributor builds QualificationProof manually
4. Contributor calls register_economic_node() manually
5. System verifies and activates
```

### Proposed (Automatic)
```
1. Contributor makes contribution (tracked automatically)
2. System detects contribution → checks thresholds
3. If threshold met → auto-generates proof from tracked data
4. System auto-registers → verifies → activates
5. Contributor notified (optional)
```

## Benefits

1. **Zero Friction**: Contributors automatically qualify when they contribute
2. **Trust-Minimized**: Uses same tracked data, no manual proof submission
3. **Consistent**: Same process for all contribution types
4. **Real-Time**: Registration happens as soon as threshold met

## Implementation Steps

1. ✅ **Contribution Tracking** (already exists)
2. ❌ **Add auto-registration service** (new)
3. ❌ **Add proof generation from tracked data** (new)
4. ❌ **Add event-driven registration triggers** (new)
5. ❌ **Add periodic batch check** (new)
6. ❌ **Add public key management** (new)
7. ❌ **Update documentation** (update)

## Code Locations

- **Contribution Tracking**: `blvm-commons/src/governance/contributions.rs`
- **Zap Tracking**: `blvm-commons/src/nostr/zap_tracker.rs`
- **Registration**: `blvm-commons/src/economic_nodes/registry.rs`
- **New Auto-Registration**: `blvm-commons/src/economic_nodes/auto_registration.rs` (to be created)

## Database Schema

**Existing Tables**:
- `unified_contributions` - tracks all contributions
- `merge_mining_contributions` - merge mining details
- `fee_forwarding_contributions` - fee forwarding details
- `zap_contributions` - zap details
- `economic_nodes` - registered nodes

**New Tables Needed**:
- `contributor_keys` - maps contributor_id to public key for veto signals
- `auto_registration_log` - tracks auto-registration events

