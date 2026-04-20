# Configuration System Consistency Analysis

## Executive Summary

**Status**: ⚠️ **INCONSISTENT** - Configuration defaults are registered but not used

The system has:
- ✅ **87+ governance variables registered** in `config_registry` with sensible defaults
- ❌ **Hardcoded values throughout codebase** that should read from config registry
- ⚠️ **Mixed approaches**: Some use YAML config, some use hardcoded values, none use config registry

---

## Problem Areas

### 1. Action Tier Thresholds

**Registered in Config Registry:**
- `tier_1_signatures_required` = 3
- `tier_1_signatures_total` = 5
- `tier_1_review_period_days` = 7
- (and similar for tiers 2-5)

**Actually Used (Hardcoded):**
- `blvm-commons/src/validation/threshold.rs`:
  - `get_tier_threshold()`: Hardcoded match statement
  - `get_tier_review_period()`: Hardcoded match statement
  - `get_threshold_for_layer()`: Hardcoded match statement
  - `get_review_period_for_layer()`: Hardcoded match statement

**Impact**: Tier thresholds cannot be changed via governance without code changes.

---

### 2. Governance Phase Thresholds

**Registered in Config Registry:**
- `phase_early_max_blocks` = 50,000
- `phase_early_max_nodes` = 10
- `phase_early_max_contributors` = 10
- (and similar for Growth/Mature phases)

**Actually Used (Hardcoded):**
- `blvm-commons/src/governance/phase_calculator.rs`:
  - `determine_phase_by_height()`: `if height < 50_000`
  - `determine_phase_by_nodes()`: `if count < 10`
  - `determine_phase_by_contributors()`: `if count < 10`

**Impact**: Phase boundaries cannot be adjusted via governance.

---

### 3. Emergency Tier Thresholds

**Registered in Config Registry:**
- `emergency_tier_1_activation_threshold` = "5-of-7"
- `emergency_tier_1_signature_threshold` = "4-of-7"
- `emergency_tier_1_max_duration_days` = 7
- (and similar for tiers 2-3)

**Actually Used (Hardcoded):**
- `blvm-commons/src/validation/emergency.rs`:
  - `review_period_days()`: Hardcoded match
  - `signature_threshold()`: Hardcoded match
  - `max_duration_days()`: Hardcoded match
  - `max_extensions()`: Hardcoded match

**Impact**: Emergency tier thresholds cannot be adjusted via governance.

---

### 4. Commons Contributor Thresholds

**Registered in Config Registry:**
- `commons_contributor_min_merge_mining_btc` = 0.01
- `commons_contributor_min_fee_forwarding_btc` = 0.1
- `commons_contributor_min_zaps_btc` = 0.01
- `commons_contributor_min_marketplace_btc` = 0.01
- `commons_contributor_measurement_period_days` = 90

**Actually Used:**
- **YAML Config**: `governance/config/commons-contributor-thresholds.yml` (human reference; optional loader support varies by branch)
- **NOT using Config Registry uniformly**: Contributor metrics may not flow through `config_registry` the same way as tier thresholds.

**Impact**: Thresholds can be edited in YAML for documentation; runtime behavior depends on whether your fork loads them—**they do not replace maintainer merge rules**.

---

### 5. Repository Layer Thresholds

**Registered in Config Registry:**
- `layer_1_2_signatures_required` = 6
- `layer_1_2_signatures_total` = 7
- `layer_1_2_review_period_days` = 180
- (and similar for layers 3-5)

**Actually Used (Hardcoded):**
- `blvm-commons/src/validation/threshold.rs`:
  - `get_threshold_for_layer()`: Hardcoded match
  - `get_review_period_for_layer()`: Hardcoded match

**Impact**: Layer thresholds cannot be adjusted via governance.

---

## Root Cause

The configuration system was designed with two separate approaches:

1. **Config Registry** (newer, governance-controlled): Variables registered in database, require Tier 5 approval to change
2. **YAML Config** (older, file-based): Commons contributor thresholds loaded from YAML files
3. **Hardcoded values in source**: Tier and emergency defaults still embedded in match statements in places

**None of the code actually reads from the config registry!**

---

## Solution Required

### Phase 1: Create Config Registry Reader Helper

Create a helper module that:
1. Reads from `ConfigRegistry` with fallback to hardcoded defaults
2. Provides type-safe accessors for common config types
3. Caches values for performance

### Phase 2: Update All Hardcoded Values

Replace hardcoded values with config registry reads:
1. `ThresholdValidator` → Read tier/layer thresholds from registry
2. `GovernancePhaseCalculator` → Read phase boundaries from registry
3. `EmergencyTier` → Read emergency thresholds from registry
4. `CommonsContributorThresholds` (if used) → Support both YAML and config registry

### Phase 3: Unify Commons Contributor Thresholds

Decide on single source of truth:
- Option A: Migrate from YAML to Config Registry only
- Option B: Support both, with Config Registry taking precedence
- Option C: Keep YAML for initial load, Config Registry for runtime changes

---

## Recommended Approach

**Option B (Hybrid)**: Support both YAML and Config Registry
- YAML provides initial defaults (easier for maintainers to review)
- Config Registry provides runtime governance-controlled changes
- Config Registry takes precedence if value exists
- Fallback to YAML if Config Registry not initialized

This allows:
- ✅ Maintainers to review defaults in YAML files
- ✅ Governance-controlled runtime adjustments
- ✅ Backward compatibility with existing YAML configs
- ✅ Gradual migration path

---

## Files That Need Updates

1. **`blvm-commons/src/validation/threshold.rs`**
   - Replace `get_tier_threshold()` with config registry read
   - Replace `get_tier_review_period()` with config registry read
   - Replace `get_threshold_for_layer()` with config registry read
   - Replace `get_review_period_for_layer()` with config registry read

2. **`blvm-commons/src/governance/phase_calculator.rs`**
   - Replace hardcoded phase boundaries with config registry read
   - Pass `ConfigRegistry` to `GovernancePhaseCalculator`

3. **`blvm-commons/src/validation/emergency.rs`**
   - Replace hardcoded emergency thresholds with config registry read
   - Pass `ConfigRegistry` to `EmergencyTier` methods

4. **`blvm-commons/src/governance/config_registry.rs`**
   - Add helper methods for type-safe value retrieval:
     - `get_i32()`, `get_f64()`, `get_string()`, `get_bool()`
   - Add caching layer for performance

---

## Implementation Priority

1. **High Priority**: Create config registry reader helper
2. **Medium Priority**: Update tier/layer thresholds
3. **Medium Priority**: Update phase calculator
4. **Low Priority**: Unify Commons contributor thresholds (YAML works for now)

---

## Testing Requirements

After implementation:
1. Verify all config values can be read from registry
2. Verify fallback to defaults works if registry not initialized
3. Verify governance changes actually take effect
4. Verify performance (caching, no excessive DB queries)
5. Integration tests for config change workflow

---

## Conclusion

**Current State**: Configuration system is **incomplete** - defaults are registered but not used.

**Required**: Complete the integration so all forkable governance variables are actually forkable at runtime via Tier 5 governance, not just registered in a database that nothing reads from.





