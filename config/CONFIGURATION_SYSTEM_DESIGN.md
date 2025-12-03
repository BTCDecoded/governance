# Configuration System Design

## Overview

The Bitcoin Commons configuration system provides a unified, type-safe interface for all governance-controlled parameters with a three-tier fallback chain:

1. **Config Registry** (Primary) - Governance-controlled, can be changed via Tier 5
2. **YAML Config** (Secondary) - File-based defaults for Commons contributors
3. **Hardcoded Defaults** (Tertiary) - Safety fallback

## Architecture

### Core Components

#### 1. `ConfigRegistry`
- **Purpose**: Database-backed registry of all governance-controlled config parameters
- **Location**: `blvm-commons/src/governance/config_registry.rs`
- **Features**:
  - Stores config keys, values, categories, tier requirements
  - Tracks change proposals and approvals
  - Requires Tier 5 governance to modify
  - Complete audit trail

#### 2. `ConfigReader`
- **Purpose**: Unified interface for reading config values with caching
- **Location**: `blvm-commons/src/governance/config_reader.rs`
- **Features**:
  - Type-safe accessors (`get_i32()`, `get_f64()`, `get_bool()`, `get_string()`)
  - In-memory caching (5-minute TTL)
  - Fallback chain support
  - Convenience methods for common patterns

#### 3. `ConfigDefaults`
- **Purpose**: Initializes all governance variables with sensible defaults
- **Location**: `blvm-commons/src/governance/config_defaults.rs`
- **Features**:
  - Registers 87+ forkable governance variables
  - Aligned with growth plan (Phase 1 → Phase 2 → Phase 3)
  - Called during system initialization

### Fallback Chain

```
Config Value Request
    ↓
1. Check Config Registry (governance-controlled)
    ↓ (if not found)
2. Check YAML Config (file-based, Commons contributors only)
    ↓ (if not found)
3. Use Hardcoded Default (safety fallback)
```

### Caching Strategy

- **Cache TTL**: 5 minutes (configurable)
- **Cache Invalidation**: 
  - Automatic after config changes are activated
  - Manual via `clear_cache()` or `invalidate_key()`
- **Cache Storage**: In-memory `HashMap<String, serde_json::Value>`

## Usage Patterns

### Basic Usage

```rust
use crate::governance::config_reader::ConfigReader;
use crate::governance::config_registry::ConfigRegistry;
use std::sync::Arc;

// Initialize
let registry = Arc::new(ConfigRegistry::new(pool));
let config = Arc::new(ConfigReader::new(registry.clone()));

// Read a value
let review_period = config.get_i32("tier_3_review_period_days", 90).await?;
let veto_threshold = config.get_f64("veto_tier_3_mining_percent", 30.0).await?;
let enabled = config.get_bool("feature_governance_enforcement", false).await?;
```

### Convenience Methods

```rust
// Get tier signatures
let (required, total) = config.get_tier_signatures(3).await?;

// Get veto thresholds
let (mining, economic) = config.get_veto_thresholds(3).await?;

// Get Commons contributor threshold (with YAML fallback)
let threshold = config.get_commons_contributor_threshold("merge_mining").await?;
```

### Integration with Validators

```rust
// ThresholdValidator with config support
let validator = ThresholdValidator::with_config(config.clone());

// Now all methods use config registry
let (req, total) = validator.get_tier_threshold(3).await?;
let review = validator.get_tier_review_period(3).await?;
```

## Configuration Categories

### 1. Action Tier Thresholds
- Signature requirements (required/total)
- Review periods (days)
- **Example**: `tier_3_signatures_required = 5`

### 2. Economic Node Veto Thresholds
- Mining hashpower percentages
- Economic activity percentages
- **Example**: `veto_tier_3_mining_percent = 30.0`

### 3. Commons Contributor Thresholds
- Minimum contribution amounts (BTC)
- Measurement periods (days)
- **Example**: `commons_contributor_min_merge_mining_btc = 0.01`

### 4. Governance Phase Thresholds
- Block height boundaries
- Economic node count boundaries
- Contributor count boundaries
- **Example**: `phase_early_max_blocks = 50000`

### 5. Repository Layer Thresholds
- Signature requirements per layer
- Review periods per layer
- **Example**: `layer_1_2_signatures_required = 6`

### 6. Emergency Tier Thresholds
- Activation thresholds
- Signature thresholds
- Duration limits
- **Example**: `emergency_tier_1_max_duration_days = 7`

### 7. Feature Flags
- Enable/disable features
- **Example**: `feature_governance_enforcement = false`

## Governance Workflow

### Changing a Configuration Value

1. **Propose Change**: Use `ConfigRegistry::propose_change()`
   - Creates a pending change proposal
   - Links to Tier 5 PR

2. **Governance Approval**: Tier 5 process
   - 180-day review period
   - 5-of-5 maintainer signatures
   - 50%+ hashpower + 60%+ economic activity support

3. **Activation**: When Tier 5 PR is merged
   - `handle_pr_merged()` detects Tier 5 PR
   - Activates approved config changes
   - Updates `current_value` in registry
   - Invalidates cache

4. **Effect**: New value takes effect immediately
   - All `ConfigReader` calls return new value
   - Cache automatically refreshed

## Migration Strategy

### Phase 1: Infrastructure (Current)
- ✅ Config registry created
- ✅ Defaults registered
- ✅ ConfigReader implemented
- ⚠️ Code still uses hardcoded values (backward compatible)

### Phase 2: Integration (Next)
- Update `ThresholdValidator` to use ConfigReader
- Update `VetoManager` to use ConfigReader
- Update `GovernancePhaseCalculator` to use ConfigReader
- Update `EmergencyTier` to use ConfigReader

### Phase 3: Unification (Future)
- Migrate Commons contributor thresholds to Config Registry
- Remove YAML config dependency (or keep as initial load only)
- All config values governance-controlled

## Backward Compatibility

All updated components maintain backward compatibility:

- **Static methods**: Old code continues to work
  - `ThresholdValidator::get_tier_threshold_static()`
  - `ThresholdValidator::get_combined_requirements_static()`

- **Instance methods**: New code uses config
  - `ThresholdValidator::with_config()` → `get_tier_threshold()`
  - `ThresholdValidator::with_config()` → `get_combined_requirements()`

## Performance Considerations

### Caching
- Config values cached for 5 minutes
- Reduces database queries
- Cache invalidated on config changes

### Async Operations
- All config reads are async
- Non-blocking database access
- Efficient concurrent access

### Fallback Performance
- Fallback chain is fast (in-memory checks)
- No performance penalty for missing configs

## Testing

### Unit Tests
- Test ConfigReader with mock registry
- Test fallback chain
- Test type conversions
- Test caching behavior

### Integration Tests
- Test with real database
- Test config change workflow
- Test cache invalidation
- Test backward compatibility

## Security Considerations

### Access Control
- Config registry requires Tier 5 governance to modify
- All changes tracked in audit trail
- No direct database access (only through registry)

### Validation
- Type checking on all reads
- Fallback to safe defaults
- Error handling for invalid values

### Audit Trail
- All config changes logged
- Change proposals tracked
- Activation timestamps recorded

## Future Enhancements

1. **Config Validation**: Schema validation for config values
2. **Config Rollback**: Ability to revert to previous values
3. **Config Diff**: Show what changed between versions
4. **Config Export**: Export current config as YAML/JSON
5. **Config Import**: Import config from YAML/JSON (with governance approval)
6. **Config Monitoring**: Alert on config changes
7. **Config History**: View historical config values

## Summary

The configuration system provides:
- ✅ **Unified Interface**: Single way to read all config values
- ✅ **Type Safety**: Type-safe accessors prevent errors
- ✅ **Governance Control**: All values forkable via Tier 5
- ✅ **Performance**: Caching reduces database load
- ✅ **Backward Compatible**: Existing code continues to work
- ✅ **Extensible**: Easy to add new config parameters

This system makes all governance variables truly forkable and adjustable at runtime through proper governance processes.





