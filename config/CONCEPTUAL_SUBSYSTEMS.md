# Conceptual Governance Subsystems

While there are 87 individual configuration variables, they can be reduced to **9 conceptual subsystems**:

## 1. Signature & Review Requirements System
**24 variables** → **1 subsystem**

This is the same conceptual system applied to two different dimensions:
- **Action Tiers** (15 vars): What signatures/review needed for Tier 1-5 changes
- **Repository Layers** (9 vars): What signatures/review needed for Layer 1-5 changes

**Concept**: "What approval requirements apply to different types of changes?"

Each tier/layer has the same 3 variables:
- `signatures_required` (N-of-M)
- `signatures_total` (M)
- `review_period_days`

## 2. Merge authorization (maintainer multisig)

**Concept**: "What signatures and review windows apply before a PR may merge?"

Enforcement follows **tier and layer** rules (and emergency procedures when applicable). **What the running code enforces** is authoritative—see `blvm-commons` validation.

## 3. Commons Contributor Qualification System
**8 variables** → **1 subsystem**

**Concept**: "What makes someone a Commons contributor for **reporting / recognition**, and how is weight computed?"

Variables (reference; not a merge gate by default):

- Minimum contribution thresholds (4 types: merge mining, fee forwarding, zaps, marketplace)
- Measurement period
- Qualification logic (OR/AND)
- Weight calculation and caps

## 4. Governance Phase Transition System
**11 variables** → **1 subsystem**

**Concept**: "When does the system transition between Early → Growth → Mature phases?"

Variables:
- Block height boundaries
- Optional operator / participation milestones (documentation only unless wired in product)
- Contributor count boundaries

## 5. Emergency Response System
**10 variables** → **1 subsystem**

**Concept**: "How do emergency tiers work and what are their limits?"

Variables:
- Activation thresholds (3 tiers)
- Signature requirements (3 tiers)
- Duration limits (3 tiers)
- Extension policies

## 6. Governance Review Policy System
**10 variables** → **1 subsystem**

**Concept**: "How are maintainers reviewed and sanctioned?"

Variables:
- Sanction thresholds (private warning, public warning, suspension, removal)
- Time limits (improvement period, appeal period, review cycle)
- Process flags (auto-escalation, evidence requirements, appeals)

## 7. Feature Flags System
**7 variables** → **1 subsystem**

**Concept**: "What features are enabled/disabled?"

Simple boolean toggles for:
- Governance enforcement
- P2P governance announcements (if used)
- Contribution tracking (analytics)
- Governance fork tooling (if used)

(Exact flag names vary by deployment; confirm behavior in `blvm-commons` for your branch.)

## 8. Network & Security Settings
**3 variables** → **1 subsystem**

**Concept**: "Basic network and security configuration"

Variables:
- Default network (mainnet/testnet/regtest)
- Formal verification requirements
- Security audit requirements

## 9. Privacy-preserving signaling (optional / protocol-level)

**Concept**: Soft-fork and adoption discussions may use privacy-preserving signaling **outside** repository merge rules.

That work is **not** the same as maintainer PR signatures. Config variables here, if any, should be documented per deployment.

---

## Summary

| Conceptual Subsystem | Individual Variables | Description |
|---------------------|---------------------|-------------|
| 1. Signature & Review Requirements | 24 | Approval requirements for tiers/layers |
| 2. Merge authorization | — | Tier/layer + emergency; aligns with §1 |
| 3. Commons Contributor Qualification | 8 | Contributor thresholds and weights |
| 4. Governance Phase Transitions | 11 | Phase boundaries |
| 5. Emergency Response | 10 | Emergency tier configuration |
| 6. Governance Review Policy | 10 | Maintainer review process |
| 7. Feature Flags | 7 | Feature toggles |
| 8. Network & Security | 3 | Basic settings |
| 9. Privacy-preserving signaling | 0+ | Optional; not merge gate |
| **TOTAL** | **87** | **9 conceptual subsystems** |

---

## Key Insight

While there are **87 individual variables**, they represent only **9 conceptual subsystems**. Most of the "variables" are just the same 3-parameter pattern (signatures_required, signatures_total, review_period_days) repeated across 5 tiers and 5 layers.

The real governance "dials" are:
1. **Approval Requirements** (signatures + review periods)
2. **Contributor metrics** (optional reporting thresholds)
3. **Phase Transitions** (maturity boundaries, if used)
4. **Emergency Response** (emergency tier limits)
5. **Review Process** (maintainer sanctions)
6. **Feature Toggles** (what's enabled in a given deployment)
7. **Security Settings** (verification/audit requirements)
8. **Protocol-level signaling** (separate from merge authorization)

Each subsystem can be adjusted independently via Tier 5 governance, but they work together to form the complete governance model.





