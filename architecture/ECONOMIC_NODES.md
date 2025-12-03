# Economic Nodes Architecture

## Overview

Economic nodes represent economic interests of Bitcoin users and provide veto mechanism for consensus-adjacent changes, ensuring governance decisions align with Bitcoin's economic incentives.

## Node Types

| Type | Qualification Criteria | Responsibilities |
|------|----------------------|------------------|
| **Mining Pools** | ≥1% network hash rate, 6+ months operational, verifiable hash rate | Monitor consensus-adjacent changes, vote on economic impact |
| **Exchanges** | ≥100 BTC daily volume (on-chain verifiable), ≥10,000 BTC holdings | Assess market impact, vote on user experience impact |
| **Custodians** | ≥$1B assets under custody, 24+ months operational, security audits | Assess custody impact, vote on security implications |

## Registration Process

**Trust-minimized, automatic activation based on cryptographic proofs.**

### Traditional Economic Nodes (Mining Pools, Exchanges, Custodians, Major Holders)

| Step | Process | Verification |
|------|---------|--------------|
| **1. Submit Registration** | Entity submits: public key, qualification proof, contact info | Self-service, no approval needed |
| **2. Cryptographic Verification** | System verifies on-chain proofs automatically | Mining pools: coinbase signatures<br>Holdings: signature challenges |
| **3. Auto-Activation** | If proofs verify → status = `active` immediately | No maintainer approval required |
| **4. Weight Calculation** | System calculates veto weight from verified proofs | Automatic, based on on-chain data |

**Code**: ```70:131:blvm-commons/src/economic_nodes/registry.rs```

### Commons Contributors (Automatic Registration)

**Current State**: Contributions are tracked automatically, but registration is manual.

**Proposed**: Automatic registration when contributions meet thresholds.

| Step | Process | Status |
|------|---------|--------|
| **1. Contribution Detected** | System automatically tracks merge mining, fee forwarding, zaps | ✅ Implemented |
| **2. Threshold Check** | System checks if 90-day contributions meet minimums | ✅ **Implemented** |
| **3. Proof Generation** | System auto-generates proof from tracked contribution data | ✅ **Implemented** |
| **4. Auto-Registration** | System automatically registers if thresholds met | ✅ **Implemented** |
| **5. Auto-Activation** | If proofs verify → status = `active` immediately | ✅ Implemented |

**Code**:
- Contribution Tracking: ```1:219:blvm-commons/src/governance/contributions.rs```
- Zap Tracking: ```1:281:blvm-commons/src/nostr/zap_tracker.rs```
- Auto-Registration: ```1:498:blvm-commons/src/economic_nodes/auto_registration.rs```
- Registration: ```70:131:blvm-commons/src/economic_nodes/registry.rs```

**Usage**: Call `CommonsContributorAutoRegistrar::check_and_register()` after recording contributions to automatically register qualified contributors.

**Details**: See [Commons Contributor Automatic Registration](./COMMONS_CONTRIBUTOR_REGISTRATION.md)

### Cryptographic Proof Requirements

| Node Type | Proof Type | Verification Method |
|----------|-----------|---------------------|
| **Mining Pools** | Coinbase signatures, block hashes | On-chain verification of mined blocks |
| **Exchanges/Custodians** | Holdings signature challenge | Cryptographic proof of address control |
| **Commons Contributors** | Merge mining blocks, fee forwarding txs, zap events, BIP70 payments | On-chain verification of contributions |

**Code**: ```220:320:blvm-commons/src/economic_nodes/registry.rs```

**Ongoing Requirements**: Nodes must maintain qualification thresholds. System automatically verifies on-chain proofs during weight recalculation.

**Detailed Proof Requirements**: See [Cryptographic Proofs](./CRYPTOGRAPHIC_PROOFS.md) for complete proof structures by entity type.

## Veto Mechanism

### Veto Power

Economic nodes can veto **Tier 3+** changes by submitting veto signals within review period. Veto requires threshold to be met (see below).

### Veto Process

1. Change notification (30-day notice for Tier 3)
2. Analysis period (15 days for economic impact assessment)
3. Veto window (15 days for signal submission)
4. Threshold check (count signals against threshold)
5. Decision (block if threshold met)

**Code**: ```113:379:blvm-commons/src/economic_nodes/veto.rs```

## Weight Calculation and Caps

### Mining Pool Weights

| Phase | Cap | Example |
|-------|-----|---------|
| Early | 10% | 35% hashpower → 0.10 weight (capped) |
| Growth | 20% | 25% hashpower → 0.20 weight (capped) |
| Mature | 10% | 35% hashpower → 0.10 weight (capped) |

**Code**: ```343:363:blvm-commons/src/economic_nodes/registry.rs```

### Other Economic Node Weights

| Type | Formula | Cap |
|------|---------|-----|
| Exchanges | `0.7 × (holdings/10K) + 0.3 × (volume/100)` | 1.0 |
| Custodians | `(holdings/10K)` | 1.0 |
| Major Holders | `(holdings/5K)` | 1.0 |

## Veto Thresholds

| Tier | Mining Threshold | Economic Threshold | Logic |
|------|------------------|---------------------|-------|
| 3 | 30%+ | 40%+ | AND (both required) |
| 4 | 25%+ | 35%+ | AND (both required) |
| 5 | 50%+ | 60%+ | AND (both required) |

### Adaptive Thresholds

Thresholds adjust automatically based on:
- **Governance Phase**: Early/Growth/Mature (block height, node count, contributor count)
- **Consolidation Metrics**: If top pool > 30%, mining threshold increases by 50%

**Code**: 
- Phase: ```157:181:blvm-commons/src/governance/phase_calculator.rs```
- Consolidation: ```140:177:blvm-commons/src/economic_nodes/consolidation.rs```

### Threshold Adjustment

Manual adjustments require Tier 5 change (5-of-5 maintainers), economic analysis, and 90-day public comment period.

## Integration with Governance

### Pull Request Processing

1. Tier classification (identify consensus-adjacent changes)
2. Node notification (alert all economic nodes)
3. Analysis period (15 days for impact assessment)
4. Veto window (15 days for signal submission)
5. Decision (block or allow based on veto threshold)

**Code**: ```19:131:blvm-commons/src/enforcement/merge_block.rs```

### Status Reporting

Economic node status reported in: GitHub status checks, Nostr events, monthly registries, audit logs.

## Security Considerations

| Aspect | Requirements |
|--------|--------------|
| **Node Security** | Hardware security modules, multi-factor authentication, incident response, regular audits |
| **Veto Security** | Cryptographic signature verification, replay protection (nonces), timestamp validation, multiple independent verifications |

**Code**: ```33:111:blvm-commons/src/economic_nodes/veto.rs```

## Economic Incentives

| Alignment Mechanisms | Disincentives |
|---------------------|---------------|
| Significant economic stake required | Excessive vetoes reduce influence |
| Better transparency = more influence | Violations result in suspension |
| Annual renewal encourages stability | Inactive nodes lose status |
| Good behavior increases influence | Public disclosure of violations |
