# Governance Configuration Default Values Reference

This document lists all 87+ governance variables and their default values as registered in the configuration system.

**Last Updated**: $(date)  
**Total Variables**: 87

---

## 1. ACTION TIER THRESHOLDS (15 variables)

### Tier 1: Routine Maintenance
- **`tier_1_signatures_required`**: `3` (out of 5)
- **`tier_1_signatures_total`**: `5`
- **`tier_1_review_period_days`**: `7`

### Tier 2: Feature Changes
- **`tier_2_signatures_required`**: `4` (out of 5)
- **`tier_2_signatures_total`**: `5`
- **`tier_2_review_period_days`**: `30`

### Tier 3: Consensus-Adjacent
- **`tier_3_signatures_required`**: `5` (out of 5)
- **`tier_3_signatures_total`**: `5`
- **`tier_3_review_period_days`**: `90`

### Tier 4: Emergency
- **`tier_4_signatures_required`**: `4` (out of 5)
- **`tier_4_signatures_total`**: `5`
- **`tier_4_review_period_days`**: `0` (immediate, no review period)

### Tier 5: Governance
- **`tier_5_signatures_required`**: `5` (out of 5)
- **`tier_5_signatures_total`**: `5`
- **`tier_5_review_period_days`**: `180`

---

## 2. ECONOMIC NODE VETO THRESHOLDS (7 variables)

### Tier 3 Veto Thresholds
- **`veto_tier_3_mining_percent`**: `30.0` (30% hashpower required)
- **`veto_tier_3_economic_percent`**: `40.0` (40% economic activity required)

### Tier 4 Veto Thresholds (Emergency)
- **`veto_tier_4_mining_percent`**: `25.0` (25% hashpower required)
- **`veto_tier_4_economic_percent`**: `35.0` (35% economic activity required)

### Tier 5 Signaling Thresholds
- **`signaling_tier_5_mining_percent`**: `50.0` (50% hashpower required for support)
- **`signaling_tier_5_economic_percent`**: `60.0` (60% economic activity required for support)

### Tier 4 Window
- **`veto_tier_4_window_hours`**: `24` (24-hour window for emergency tier)

---

## 3. COMMONS CONTRIBUTOR THRESHOLDS (8 variables)

### Minimum Contribution Amounts (BTC)
- **`commons_contributor_min_merge_mining_btc`**: `0.01` (0.01 BTC)
- **`commons_contributor_min_fee_forwarding_btc`**: `0.1` (0.1 BTC)
- **`commons_contributor_min_zaps_btc`**: `0.01` (0.01 BTC)
- **`commons_contributor_min_marketplace_btc`**: `0.01` (0.01 BTC)

### Measurement Period
- **`commons_contributor_measurement_period_days`**: `90` (90 days)

### Qualification Logic
- **`commons_contributor_qualification_logic`**: `"OR"` (meet any threshold)

### Weight Calculation
- **`commons_contributor_weight_formula`**: `"linear"` (linear weight calculation)
- **`commons_contributor_weight_cap`**: `0.10` (10% maximum weight per contributor)

---

## 4. GOVERNANCE PHASE THRESHOLDS (11 variables)

### Early Phase Boundaries
- **`phase_early_max_blocks`**: `50000` (50,000 blocks)
- **`phase_early_max_nodes`**: `10` (10 economic nodes)
- **`phase_early_max_contributors`**: `10` (10 Commons contributors)

### Growth Phase Boundaries
- **`phase_growth_min_blocks`**: `50000` (50,000 blocks)
- **`phase_growth_max_blocks`**: `200000` (200,000 blocks)
- **`phase_growth_min_nodes`**: `10` (10 economic nodes)
- **`phase_growth_max_nodes`**: `30` (30 economic nodes)
- **`phase_growth_min_contributors`**: `10` (10 Commons contributors)
- **`phase_growth_max_contributors`**: `100` (100 Commons contributors)

### Mature Phase Boundaries
- **`phase_mature_min_blocks`**: `200000` (200,000 blocks)
- **`phase_mature_min_nodes`**: `30` (30 economic nodes)
- **`phase_mature_min_contributors`**: `100` (100 Commons contributors)

---

## 5. REPOSITORY LAYER THRESHOLDS (9 variables)

### Layer 1 & 2 (Constitutional Layers)
- **`layer_1_2_signatures_required`**: `6` (out of 7)
- **`layer_1_2_signatures_total`**: `7`
- **`layer_1_2_review_period_days`**: `180`

### Layer 3 (Implementation Layer)
- **`layer_3_signatures_required`**: `4` (out of 5)
- **`layer_3_signatures_total`**: `5`
- **`layer_3_review_period_days`**: `90`

### Layer 4 (Application Layer)
- **`layer_4_signatures_required`**: `3` (out of 5)
- **`layer_4_signatures_total`**: `5`
- **`layer_4_review_period_days`**: `60`

### Layer 5 (Extension Layer)
- **`layer_5_signatures_required`**: `2` (out of 3)
- **`layer_5_signatures_total`**: `3`
- **`layer_5_review_period_days`**: `14`

---

## 6. EMERGENCY TIER THRESHOLDS (10 variables)

### Emergency Tier 1: Critical
- **`emergency_tier_1_activation_threshold`**: `"5-of-7"` (5 of 7 emergency keyholders)
- **`emergency_tier_1_signature_threshold`**: `"4-of-7"` (4 of 7 signatures for PRs)
- **`emergency_tier_1_max_duration_days`**: `7` (7 days maximum)

### Emergency Tier 2: Urgent
- **`emergency_tier_2_activation_threshold`**: `"5-of-7"` (5 of 7 emergency keyholders)
- **`emergency_tier_2_signature_threshold`**: `"5-of-7"` (5 of 7 signatures for PRs)
- **`emergency_tier_2_review_period_days`**: `7` (7 days review)
- **`emergency_tier_2_max_duration_days`**: `30` (30 days maximum)
- **`emergency_tier_2_max_extensions`**: `1` (1 extension allowed)

### Emergency Tier 3: Elevated
- **`emergency_tier_3_activation_threshold`**: `"5-of-7"` (5 of 7 emergency keyholders)
- **`emergency_tier_3_signature_threshold`**: `"6-of-7"` (6 of 7 signatures for PRs)
- **`emergency_tier_3_review_period_days`**: `30` (30 days review)
- **`emergency_tier_3_max_duration_days`**: `90` (90 days maximum)
- **`emergency_tier_3_max_extensions`**: `2` (2 extensions allowed)

---

## 7. GOVERNANCE REVIEW POLICY (10 variables)

### Sanction Thresholds
- **`governance_review_private_warning_threshold`**: `3` (3 violations)
- **`governance_review_public_warning_threshold`**: `5` (5 violations)
- **`governance_review_suspension_threshold`**: `7` (7 violations)
- **`governance_review_removal_threshold`**: `10` (10 violations)

### Time Limits
- **`governance_review_improvement_period_days`**: `90` (90 days to improve)
- **`governance_review_appeal_period_days`**: `30` (30 days to appeal)
- **`governance_review_review_cycle_days`**: `180` (180 days review cycle)

### Process Configuration
- **`governance_review_auto_escalation`**: `true` (auto-escalate violations)
- **`governance_review_require_evidence`**: `true` (require evidence for sanctions)
- **`governance_review_allow_appeals`**: `true` (allow appeals)

---

## 8. FEATURE FLAGS (7 variables)

- **`feature_governance_enforcement`**: `false` (disabled in Phase 1, enable in Phase 2)
- **`feature_p2p_governance`**: `true` (P2P governance enabled)
- **`feature_economic_nodes`**: `true` (Economic node system enabled)
- **`feature_contribution_tracking`**: `true` (Contribution tracking enabled)
- **`feature_auto_registration`**: `false` (Auto-registration disabled initially)
- **`feature_veto_system`**: `true` (Veto system enabled)
- **`feature_fork_system`**: `true` (Fork system enabled)

---

## 9. NETWORK & SECURITY (3 variables)

- **`network_default`**: `"mainnet"` (Default Bitcoin network)
- **`security_require_formal_verification_layer_2`**: `true` (Require formal verification for Layer 2)
- **`security_require_audit_tier_3_plus`**: `true` (Require audit for Tier 3+ changes)

---

## Summary by Category

| Category | Variables | Description |
|----------|-----------|-------------|
| Action Tier Thresholds | 15 | Signature requirements and review periods for Tiers 1-5 |
| Economic Node Veto Thresholds | 7 | Mining and economic activity percentages for veto/support |
| Commons Contributor Thresholds | 8 | Minimum contributions, measurement periods, weight calculation |
| Governance Phase Thresholds | 11 | Block height, node count, contributor count boundaries |
| Repository Layer Thresholds | 9 | Signature requirements and review periods for Layers 1-5 |
| Emergency Tier Thresholds | 10 | Activation, signature, duration thresholds for emergency tiers |
| Governance Review Policy | 10 | Sanction thresholds, time limits, appeal processes |
| Feature Flags | 7 | Core feature toggles |
| Network & Security | 3 | Default network, security requirements |
| **TOTAL** | **87** | **All forkable governance variables** |

---

## Default Value Rationale

### Phase 1 (Current) - Conservative Defaults
- **Signature Requirements**: High (5-of-5 for Tier 3+, 6-of-7 for Layers 1-2)
- **Review Periods**: Long (90-180 days for Tier 3-5)
- **Veto Thresholds**: Moderate (30%+40% for Tier 3)
- **Commons Contributors**: Low thresholds (0.01 BTC) to encourage participation
- **Feature Flags**: Governance enforcement disabled initially

### Alignment with Growth Plan
- **Early Phase**: < 50K blocks, < 10 nodes, < 10 contributors
- **Growth Phase**: 50K-200K blocks, 10-30 nodes, 10-100 contributors
- **Mature Phase**: 200K+ blocks, 30+ nodes, 100+ contributors

### Security Focus
- High signature requirements prevent single points of failure
- Long review periods allow thorough deliberation
- Multiple veto mechanisms (mining + economic) require coordination
- Emergency tiers have strict activation requirements (5-of-7 keyholders)

---

## Changing Default Values

All default values can be changed via Tier 5 governance:

1. **Propose Change**: Use `ConfigRegistry::propose_change()`
2. **Create Tier 5 PR**: Link change to PR
3. **Governance Approval**: 180 days, 5-of-5 maintainers, 50%+ hashpower + 60%+ economic
4. **Activation**: Automatic on PR merge
5. **Effect**: New value takes effect immediately

---

## Notes

- All values require **Tier 5 governance approval** to change
- Defaults are **conservative** for Phase 1 (infrastructure building)
- Values can be **adjusted** in Phase 2-3 based on real-world experience
- All changes are **tracked** in audit trail
- Cache is **automatically invalidated** when changes activated

---

**For detailed information about each variable, see `FORKABLE_VARIABLES.md`**





