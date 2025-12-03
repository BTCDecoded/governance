# Cryptographic Proof Requirements by Entity Type

## Overview

Each economic node type must submit different cryptographic proofs for trust-minimized auto-activation. Proofs vary by entity type and are verified automatically (no maintainer approval).

**Code**: ```239:369:blvm-commons/src/economic_nodes/types.rs```

## Proof Requirements by Type

| Entity Type | Required Proof | Cryptographic Verification | Trust Level |
|------------|----------------|---------------------------|-------------|
| **Mining Pool** | `HashpowerProof` | Coinbase signatures, block hashes | Fully trustless (on-chain) |
| **Exchange** | `HoldingsProof` | Signature challenge (address control) | Fully trustless (cryptographic) |
| **Custodian** | `HoldingsProof` | Signature challenge (address control) | Fully trustless (cryptographic) |
| **Major Holder** | `HoldingsProof` | Signature challenge (address control) | Fully trustless (cryptographic) |
| **Commons Contributor** | `CommonsContributorProof` (one or more) | On-chain proofs (varies by contribution type) | Fully trustless (on-chain) |

## Detailed Proof Structures

### 1. Mining Pools

**Proof Type**: `HashpowerProof`

```rust
{
  blocks_mined: Vec<String>,        // Block hashes (on-chain)
  time_period_days: u32,            // Measurement period (30 days)
  total_network_blocks: u32,         // Total blocks in period
  percentage: f64                    // Hashpower percentage
}
```

**Verification**:
- System verifies block hashes exist on-chain
- Coinbase signatures prove mining (same keys used for veto signals)
- 30-day rolling average prevents gaming

**Code**: ```336:352:blvm-commons/src/economic_nodes/registry.rs```

### 2. Exchanges / Custodians / Major Holders

**Proof Type**: `HoldingsProof`

```rust
{
  addresses: Vec<String>,            // Bitcoin addresses
  total_btc: f64,                    // Total holdings
  signature_challenge: String        // Signature proving control
}
```

**Verification**:
- Signature challenge: Entity signs `public_key || addresses`
- Proves cryptographic control of claimed addresses
- Anyone can verify signature independently

**Code**: ```354:381:blvm-commons/src/economic_nodes/registry.rs```

### 3. Commons Contributors

**Proof Type**: `CommonsContributorProof` (one or more of):

#### 3a. Merge Mining Proof

```rust
{
  total_revenue_btc: f64,
  period_days: u32,                  // 90-day period
  blocks_mined: Vec<MergeMiningBlockProof>,
  contributor_id: String
}

MergeMiningBlockProof {
  block_hash: String,                // Secondary chain block
  chain_id: String,
  commons_fee_amount: u64,           // Satoshis
  coinbase_signature: String         // On-chain signature
}
```

**Verification**: On-chain coinbase signatures, secondary chain blocks

#### 3b. Fee Forwarding Proof

```rust
{
  total_fees_forwarded_btc: f64,
  period_days: u32,                  // 90-day period
  blocks_with_forwarding: Vec<FeeForwardingBlockProof>,
  contributor_id: String
}

FeeForwardingBlockProof {
  block_hash: String,
  block_height: u32,
  forwarded_amount: u64,             // Satoshis
  commons_address: String,
  tx_hash: String                    // On-chain transaction
}
```

**Verification**: On-chain transactions to Commons address

#### 3c. Zap Proof (Lightning + Nostr)

```rust
{
  total_zaps_btc: f64,
  period_days: u32,                  // 90-day period
  zap_events: Vec<ZapEventProof>,
  contributor_id: String              // Nostr pubkey
}

ZapEventProof {
  nostr_event_id: String,            // Nostr event ID
  zap_amount: u64,                   // Satoshis
  payment_hash: String,              // Lightning payment hash
  timestamp: i64
}
```

**Verification**: Nostr event + Lightning payment proof

#### 3d. Marketplace Sales Proof (BIP70)

```rust
{
  total_sales_btc: f64,              // BIP70 payments (BTC)
  period_days: u32,                  // 90-day period
  module_payments: Vec<ModulePaymentProof>,
  contributor_id: String
}

ModulePaymentProof {
  payment_id: String,
  module_id: String,
  amount_btc: f64,                   // BIP70 payment (BTC)
  payment_hash: String,               // BIP70 payment hash
  timestamp: i64
}
```

**Verification**: BIP70 payment records (on-chain)

**Code**: ```383:434:blvm-commons/src/economic_nodes/registry.rs```

## Registration Flow

1. **Entity submits**: `QualificationProof` with appropriate proof type(s)
2. **System verifies**: Cryptographic proofs automatically
3. **Auto-activation**: If proofs verify → `status = 'active'` immediately
4. **No maintainer approval**: Trust-minimized, algorithmic verification

**Code**: ```70:151:blvm-commons/src/economic_nodes/registry.rs```

## Maintainers (Not Economic Nodes)

**Note**: Maintainers are separate from economic nodes. They sign PRs, not economic node registrations.

- Maintainers: Sign PRs with governance keys (Tier-based thresholds)
- Economic Nodes: Submit cryptographic proofs for registration (auto-activation)

## Verification Status

| Proof Type | Verification Status | Notes |
|-----------|---------------------|-------|
| Mining pool block hashes | ✅ Structural validation | TODO: Full blockchain verification |
| Holdings signature challenge | ✅ Cryptographic verification | Fully implemented |
| Merge mining blocks | ✅ Structural validation | TODO: Full blockchain verification |
| Fee forwarding transactions | ✅ Structural validation | TODO: Full blockchain verification |
| Zap events | ✅ Structural validation | TODO: Nostr/Lightning verification |
| BIP70 payments | ✅ Structural validation | TODO: BIP70 verification |

**Code**: ```330:443:blvm-commons/src/economic_nodes/registry.rs```

## Summary

- **Mining Pools**: Block hashes + coinbase signatures (on-chain)
- **Holdings-based** (Exchange/Custodian/Major Holder): Signature challenge (cryptographic)
- **Commons Contributors**: On-chain proofs (merge mining, fee forwarding, zaps, BIP70)

All proofs are verified automatically. If cryptographic proofs verify, activation is immediate (no maintainer approval).

