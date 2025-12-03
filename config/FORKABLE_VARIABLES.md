# Forkable Governance Variables

This document lists all governance variables that are forkable (can be customized in different governance rulesets) and their default values for the default Commons distribution.

## Overview

All variables listed here are registered in the `governance_config_registry` table and require **Tier 5 governance approval** to change. This ensures that changes to governance parameters themselves go through the most rigorous process.

## Default Values Rationale

Default values are set conservatively for **Phase 1 (Infrastructure Building)** and are appropriate for:
- Early adoption (fewer economic nodes)
- Conservative security posture
- Gradual growth trajectory

As the system matures through Phase 2 → Phase 3, these values can be adjusted via Tier 5 governance to reflect:
- Increased economic node participation
- Mature ecosystem dynamics
- Optimized thresholds based on real-world experience

---

## 1. Action Tier Thresholds

### Tier 1: Routine Maintenance
- **`tier_1_signatures_required`**: `3` (out of 5)
- **`tier_1_signatures_total`**: `5`
- **`tier_1_review_period_days`**: `7`

**Rationale**: Low threshold for routine work, short review period.

### Tier 2: Feature Changes
- **`tier_2_signatures_required`**: `4` (out of 5)
- **`tier_2_signatures_total`**: `5`
- **`tier_2_review_period_days`**: `30`

**Rationale**: Higher threshold for new features, month-long review.

### Tier 3: Consensus-Adjacent
- **`tier_3_signatures_required`**: `5` (out of 5)
- **`tier_3_signatures_total`**: `5`
- **`tier_3_review_period_days`**: `90`

**Rationale**: Unanimous approval required, 90-day review period, economic node veto applies.

### Tier 4: Emergency Actions
- **`tier_4_signatures_required`**: `4` (out of 5)
- **`tier_4_signatures_total`**: `5`
- **`tier_4_review_period_days`**: `0`

**Rationale**: Fast response for emergencies, but still requires majority approval.

### Tier 5: Governance Changes
- **`tier_5_signatures_required`**: `5` (out of 5)
- **`tier_5_signatures_total`**: `5`
- **`tier_5_review_period_days`**: `180`

**Rationale**: Constitutional changes require longest review period (6 months) and unanimous maintainer approval.

---

## 2. Economic Node Veto Thresholds

### Tier 3 Veto Thresholds
- **`veto_tier_3_mining_percent`**: `30.0%`
- **`veto_tier_3_economic_percent`**: `40.0%`

**Rationale**: Requires coordination between miners AND economic nodes (AND logic). Prevents single-group veto.

### Tier 4 Veto Thresholds (Emergency)
- **`veto_tier_4_mining_percent`**: `25.0%`
- **`veto_tier_4_economic_percent`**: `35.0%`
- **`veto_tier_4_window_hours`**: `24`

**Rationale**: Lower thresholds for emergency actions, but shorter window (24 hours).

### Tier 5 Signaling Thresholds
- **`signaling_tier_5_mining_percent`**: `50.0%`
- **`signaling_tier_5_economic_percent`**: `60.0%`

**Rationale**: Governance changes require active support (not just lack of opposition). Higher thresholds than veto.

---

## 3. Commons Contributor Thresholds

### Measurement Period
- **`commons_contributor_measurement_period_days`**: `90`

**Rationale**: 90-day rolling window balances responsiveness with stability.

### Qualification Logic
- **`commons_contributor_qualification_logic`**: `"OR"`

**Rationale**: Any threshold met qualifies (inclusive approach).

### Contribution Thresholds (BTC over 90-day period)
- **`commons_contributor_min_merge_mining_btc`**: `0.01 BTC`
- **`commons_contributor_min_fee_forwarding_btc`**: `0.1 BTC`
- **`commons_contributor_min_zaps_btc`**: `0.01 BTC`
- **`commons_contributor_min_marketplace_btc`**: `0.01 BTC`

**Rationale**: Conservative thresholds to encourage participation while maintaining meaningful economic commitment. Can be adjusted as ecosystem grows.

### Weight Calculation
- **`commons_contributor_weight_normalization_factor`**: `1.0` (1 BTC = 1.0 weight)
- **`commons_contributor_min_weight`**: `0.01` (prevents dust)

**Rationale**: Quadratic weighting prevents whale dominance while rewarding contribution.

---

## 4. Governance Phase Calculation Thresholds

These determine when the system transitions between **Early → Growth → Mature** phases.

### Early Phase Maximums
- **`phase_early_max_blocks`**: `50,000` (~1 year)
- **`phase_early_max_nodes`**: `10`
- **`phase_early_max_contributors`**: `10`

### Growth Phase Ranges
- **`phase_growth_min_blocks`**: `50,000`
- **`phase_growth_max_blocks`**: `200,000` (~4 years)
- **`phase_growth_min_nodes`**: `10`
- **`phase_growth_max_nodes`**: `30`
- **`phase_growth_min_contributors`**: `10`
- **`phase_growth_max_contributors`**: `100`

### Mature Phase Minimums
- **`phase_mature_min_blocks`**: `200,000`
- **`phase_mature_min_nodes`**: `30`
- **`phase_mature_min_contributors`**: `100`

**Rationale**: Aligned with growth plan projections:
- Year 1: ~52K blocks, ~5-10 nodes → **Growth Phase**
- Year 2: ~105K blocks, ~10-20 nodes → **Growth Phase**
- Year 3: ~157K blocks, ~20-30 nodes → **Mature Phase**
- Year 4+: ~210K+ blocks, ~30+ nodes → **Mature Phase**

---

## 5. Repository Layer Thresholds

### Layer 1-2: Constitutional (Orange Paper, Consensus Proof)
- **`layer_1_2_signatures_required`**: `6` (out of 7)
- **`layer_1_2_signatures_total`**: `7`
- **`layer_1_2_review_period_days`**: `180`

**Rationale**: Highest security for constitutional layer.

### Layer 3: Protocol Engine
- **`layer_3_signatures_required`**: `4` (out of 5)
- **`layer_3_signatures_total`**: `5`
- **`layer_3_review_period_days`**: `90`

**Rationale**: Core protocol implementation requires significant review.

### Layer 4: Reference Node
- **`layer_4_signatures_required`**: `3` (out of 5)
- **`layer_4_signatures_total`**: `5`
- **`layer_4_review_period_days`**: `60`

**Rationale**: Application layer has lower threshold but still requires review.

### Layer 5: Developer SDK
- **`layer_5_signatures_required`**: `2` (out of 3)
- **`layer_5_signatures_total`**: `3`
- **`layer_5_review_period_days`**: `14`

**Rationale**: Tools layer has lowest threshold for faster iteration.

---

## 6. Emergency Tier Thresholds

### Emergency Tier 1: Critical
- **`emergency_tier_1_activation_threshold`**: `"5-of-7"` (emergency keyholders)
- **`emergency_tier_1_signature_threshold`**: `"4-of-7"` (for PRs)
- **`emergency_tier_1_max_duration_days`**: `7`

**Rationale**: Network-threatening issues require fast response but limited duration.

### Emergency Tier 2: Urgent
- **`emergency_tier_2_activation_threshold`**: `"5-of-7"`
- **`emergency_tier_2_signature_threshold`**: `"5-of-7"`
- **`emergency_tier_2_review_period_days`**: `7`
- **`emergency_tier_2_max_duration_days`**: `30`
- **`emergency_tier_2_max_extensions`**: `1`

**Rationale**: Serious security issues with 7-day review, 30-day max duration.

### Emergency Tier 3: Elevated
- **`emergency_tier_3_activation_threshold`**: `"5-of-7"`
- **`emergency_tier_3_signature_threshold`**: `"6-of-7"`
- **`emergency_tier_3_review_period_days`**: `30`
- **`emergency_tier_3_max_duration_days`**: `90`
- **`emergency_tier_3_max_extensions`**: `2`

**Rationale**: Important priorities with longer review and duration, allows extensions.

---

## 7. Governance Review Policy Thresholds

### Sanction Thresholds
- **`governance_review_private_warning_threshold`**: `"4-of-7"`
- **`governance_review_public_warning_threshold`**: `"5-of-7"`
- **`governance_review_removal_threshold`**: `"6-of-7"`
- **`governance_review_inter_team_removal_threshold`**: `"4-of-7"` (teams)

**Rationale**: Graduated sanctions with high thresholds to prevent abuse.

### Time Limits
- **`governance_review_improvement_period_days`**: `90`
- **`governance_review_response_deadline_days`**: `30`
- **`governance_review_resolution_deadline_days`**: `180`
- **`governance_review_appeal_deadline_days`**: `60`
- **`governance_review_mediation_period_days`**: `30`

**Rationale**: Balanced time limits for due process without indefinite delays.

### Emergency Removal
- **`governance_review_emergency_removal_threshold`**: `"4-of-5"` (emergency keyholders)

**Rationale**: Lower threshold for immediate security threats.

---

## 8. Feature Flags

### Core Features
- **`feature_governance_enforcement`**: `false` (Phase 1 default, activates in Phase 2)
- **`feature_p2p_governance`**: `true`
- **`feature_economic_node_veto`**: `true`
- **`feature_commons_contributor_auto_registration`**: `true`
- **`feature_governance_fork`**: `true`
- **`feature_merkle_veto_proofs`**: `true`
- **`feature_privacy_preserving_votes`**: `true`

**Rationale**: Most features enabled by default, but governance enforcement disabled until Phase 2 activation.

---

## 9. Network & Security Configuration

- **`network_default`**: `"mainnet"`
- **`security_audit_required_tier_3`**: `true`
- **`security_formal_verification_required_layer_2`**: `true`

**Rationale**: Security requirements enabled by default.

---

## Growth Plan Alignment

### Phase 1 (Current): Infrastructure Building
- **Status**: All defaults registered, conservative values
- **Governance Enforcement**: Disabled (`feature_governance_enforcement = false`)
- **Rationale**: System is being built and tested

### Phase 2 (3-6 months): Governance Activation
- **Expected Changes**:
  - Enable `feature_governance_enforcement = true`
  - Adjust thresholds based on initial economic node participation
  - Fine-tune Commons contributor thresholds based on actual contribution patterns

### Phase 3 (12+ months): Full Operation
- **Expected Changes**:
  - Optimize thresholds based on real-world experience
  - Adjust phase calculation thresholds if growth differs from projections
  - Refine veto thresholds based on actual coordination patterns

---

## How to Change These Values

1. **Propose Change**: Use `ConfigRegistry::propose_change()` or create Tier 5 PR
2. **Governance Approval**: Requires Tier 5 process (180-day review, 5-of-5 maintainers, 50%+ hashpower + 60%+ economic activity support)
3. **Activation**: Change is activated when Tier 5 PR is merged
4. **Audit Trail**: All changes recorded in `governance_config_history` table

---

## Total Variables Registered

**~80+ forkable governance variables** covering:
- Action tier thresholds (15 variables)
- Economic node veto thresholds (7 variables)
- Commons contributor thresholds (8 variables)
- Governance phase thresholds (11 variables)
- Repository layer thresholds (9 variables)
- Emergency tier thresholds (10 variables)
- Governance review policy thresholds (10 variables)
- Feature flags (7 variables)
- Network & security (3 variables)

All variables are forkable and can be customized in alternative governance rulesets.





