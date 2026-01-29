# BTCDecoded Governance Process

## ⚠️ ACTIVATION STATUS

**Current Status: Phase 1 (Infrastructure Building)**

- ✅ **Infrastructure Complete**: All core components implemented
- ⚠️ **Not Yet Activated**: Governance rules are not enforced
- 🔧 **Test Keys Only**: No real cryptographic enforcement
- 📋 **Development Phase**: System is in rapid AI-assisted development

**Timeline:**
- **Phase 2 Activation**: 3-6 months (governance enforcement begins)
- **Phase 3 Full Operation**: 12+ months (mature, stable system)

## Constitutional Governance Model

Bitcoin Commons implements a **5-tier constitutional governance system** that makes Bitcoin governance **6x harder to capture** than Bitcoin Core's current model, with **complete transparency** through cryptographic audit trails and **user-protective** mechanisms.

**Core Innovation:** Apply the same cryptographic enforcement to governance that Bitcoin applies to consensus - making power visible, capture expensive, and exit cheap.

## How Governance Works

### Action Tiers (Constitutional Model)

**Tier 1: Routine Maintenance** (3-of-5, 7 days)
- Bug fixes, documentation, performance optimizations
- Non-consensus changes only

**Tier 2: Feature Changes** (4-of-5, 30 days)  
- New RPC methods, P2P changes, wallet features
- Must include technical specification

**Tier 3: Consensus-Adjacent** (5-of-5, 90 days + economic node veto)
- Changes affecting consensus validation code
- Economic nodes can veto (30%+ hashpower AND 40%+ economic activity)

**Tier 4: Emergency Actions** (4-of-5, 0 days review period)
- Critical security patches, network-threatening bugs
- Real-time economic node oversight, post-mortem required

**Tier 5: Governance Changes** (Special process, 180 days)
- Changes to governance rules themselves
- Requires economic node signaling (50%+ hashpower, 60%+ economic activity)

### Pull Request Process

1. Developer opens PR
   - **Code**: `blvm-commons/src/webhooks/pull_request.rs:handle_pull_request()`
2. Governance App classifies tier automatically (with temp. manual override)
   - **Code**: `blvm-commons/src/validation/tier_classification.rs:classify_tier()`
3. Maintainers review and sign: `/governance-sign <signature>`
   - **Code**: `blvm-commons/src/webhooks/comment.rs:handle_governance_sign()`
4. Review period elapses (tier-specific duration)
   - **Code**: `blvm-commons/src/validation/review_period.rs:check_review_period()`
5. Economic node veto period (Tier 3+)
   - **Code**: `blvm-commons/src/economic_nodes/veto.rs:check_veto_threshold()`
6. Requirements met → merge enabled
   - **Code**: `blvm-commons/src/enforcement/merge_block.rs:should_block_merge()`
7. PR merged

**See [HOW_TO.md](HOW_TO.md) for detailed step-by-step instructions.**

### Signature Requirements by Layer

- **Layer 1-2 (Constitutional)**: 6-of-7 maintainers, 180 days (365 for consensus changes)
- **Layer 3 (Implementation)**: 4-of-5 maintainers, 90 days
- **Layer 4 (Application)**: 3-of-5 maintainers, 60 days
- **Layer 5 (Extension)**: 2-of-3 maintainers, 14 days

**Note**: When both Layer and Tier requirements apply, the system uses the "most restrictive wins" rule. See [LAYER_TIER_MODEL.md](LAYER_TIER_MODEL.md) for detailed combination rules.

### Layer + Tier Combination

The governance system combines two dimensions:

1. **Layers** (Repository Architecture) - Which repository the change affects
2. **Tiers** (Action Classification) - What type of change is being made

When both apply, the system takes the most restrictive (highest) requirements:

| Example | Layer | Tier | Final Signatures | Final Review | Source |
|---------|-------|------|------------------|--------------|---------|
| Bug fix in blvm-protocol | 3 | 1 | 4-of-5 | 90 days | Layer 3 |
| New feature in blvm-sdk | 5 | 2 | 4-of-5 | 30 days | Tier 2 |
| Consensus change in blvm-spec | 1 | 3 | 6-of-7 | 180 days | Layer 1 |
| Emergency fix in blvm-node | 4 | 4 | 4-of-5 | 0 days | Tier 4 |

See [LAYER_TIER_MODEL.md](LAYER_TIER_MODEL.md) for the complete decision matrix.

### Emergency Tier System

Bitcoin Commons uses a three-tiered emergency response system for proportional handling of critical issues.

#### Tier 1: Critical Emergency (Network-Threatening)

**Activation Criteria:**
- Inflation bugs (CVE-2010-5139 class)
- Consensus fork risks (CVE-2018-17144 class)
- P2P network DoS vulnerabilities
- Remote code execution
- Private key extraction

**Requirements:**
- 0 day review period
- 4-of-7 maintainer signatures
- 5-of-7 emergency keyholders to activate
- 7 day maximum duration
- No extensions allowed

**Post-Activation:**
- Post-mortem required within 30 days
- Security audit required within 60 days
- Public disclosure after patch deployment

**Historical Examples:**
- **CVE-2010-5139** (2010): Value overflow allowing creation of 184B BTC. Fixed in 5 hours with hard fork.
- **CVE-2018-17144** (2018): Inflation bug allowing double-spend of same input. Same-day patch, coordinated disclosure.

**Rationale:** Some vulnerabilities threaten network survival and require immediate action. Historical incidents show response times measured in hours, not days or weeks. Tier 1 enables this while maintaining multi-signature security (4-of-7).

#### Tier 2: Urgent Security Issue

**Activation Criteria:**
- Memory corruption vulnerabilities
- Privacy leaks (transaction linkage)
- Crash exploits (non-DoS)
- Privilege escalation
- Data corruption bugs

**Requirements:**
- 7 day review period
- 5-of-7 maintainer signatures
- 5-of-7 emergency keyholders to activate
- 30 day maximum duration
- One extension allowed (30 days, requires 6-of-7)

**Post-Activation:**
- Post-mortem required within 60 days
- Public disclosure after majority node deployment

**Historical Examples:**
- **BIP66 Consensus Fork** (2015): Non-upgraded miners accepted invalid block. Required urgent but not immediate coordination over hours/days.

#### Tier 3: Elevated Priority

**Activation Criteria:**
- Competitive response (other implementations advancing)
- Important bug fixes (non-security)
- Performance degradation issues
- Ecosystem compatibility problems
- User experience issues affecting adoption

**Requirements:**
- 30 day review period
- 6-of-7 maintainer signatures
- 5-of-7 emergency keyholders to activate
- 90 day maximum duration
- Two extensions allowed (30 days each, requires 6-of-7)

**Post-Activation:**
- Post-mortem required within 90 days
- Immediate public disclosure

#### Emergency Activation Process

1. Emergency keyholder submits activation request with evidence
2. Other emergency keyholders review and sign (5-of-7 required)
3. Governance App activates tier and adjusts requirements
4. Status checks reflect emergency parameters
5. PRs merged under emergency rules
6. Post-activation requirements tracked
7. Automatic expiration at max duration unless extended

#### Safeguards

**Abuse Prevention:**
- All emergency activations logged in governance repository
- Post-mortem required for accountability
- Tier downgrades if criteria not met
- Community oversight via public disclosure

**Automatic Expiration:**
- No indefinite emergency modes
- Extensions require higher thresholds (6-of-7 vs 5-of-7)
- Multiple extensions discouraged

**Escalation Path:**
- Start with appropriate tier based on evidence
- Can escalate if situation worsens
- Cannot downgrade active emergency without resolution

See `emergency-tiers.yml` for complete configuration.

### Consensus Rule Changes

**Important:** BTCDecoded governance is **advisory only** for Bitcoin protocol consensus changes. Maintainers cannot force network adoption.

#### Scope Clarification

**What We Control (Repository Governance):**
- Merge access to BTCDecoded repositories
- Maintainer selection and removal
- Official release creation
- Code quality standards

**What We Don't Control (Protocol Governance):**
- Bitcoin network consensus rules
- User adoption decisions
- Node operator choices
- Miner signaling

#### Consensus Change Process

When changes affect consensus rules (`consensus-rules/**`, `validation/**`, `block-acceptance/**`):

**Repository Requirements (Binding):**
- 6-of-7 maintainer signatures
- 365 day review period
- BIP specification required
- Comprehensive test vectors required
- Security audit required
- Equivalence proof required (mathematical correctness)

**User Activation (Advisory Only):**

1. **Code Approved**: Maintainers approve with 6-of-7 signatures
2. **Code Released**: Published as optional upgrade
3. **Users Signal**: Node operators choose whether to upgrade
4. **Activation Decision**: Based on network signaling thresholds

**Recommended Thresholds (Advisory):**
- 75% node adoption
- 90% hash power signaling
- Economic majority (e.g., 5 of top 10 exchanges)

**Measurement:**
- BIP9-style version bits or node polling
- 90-day measurement period

**Clarification:** Maintainers approve code for release. Users decide whether to run it. No amount of maintainer signatures forces network adoption. Users retain sovereignty to fork, run alternatives, or reject changes.

See `SCOPE.md` for detailed explanation of repository vs. protocol governance.

## Formal Verification Requirements

### Technical Prerequisites for Consensus Changes

BTCDecoded implements **mathematical verification** of consensus code to prevent capture and ensure correctness. This creates an objective, non-negotiable technical barrier that complements social governance.

#### Verification Stack

1. **Kani Model Checking** (required)
   - Symbolic verification with bounded model checking
   - Proves mathematical invariants hold for all possible inputs
   - Cannot be bypassed or overridden

2. **Property-Based Testing** (required)
   - Randomized testing with `proptest`
   - Discovers edge cases through fuzzing
   - Complements Kani with empirical coverage

3. **Mathematical Specifications** (required)
   - Formal documentation of consensus rules
   - Invariants documented in code
   - Traceability to Orange Paper

#### Enforcement Levels

**Level 1: CI Enforcement (Ostrom #4: Monitoring)**
- Automated verification runs on every PR
- Blocks merge if verification fails
- No human override possible
- Technical correctness is non-negotiable

**Level 2: Governance App (Ostrom #5: Graduated Sanctions)**
- Validates verification passed before allowing signatures
- PRs without passing verification cannot progress
- Prevents maintainers from signing unverified code

**Level 3: Meta-Governance (Ostrom #3: Collective Choice)**
- Verification requirements set by maintainers collectively
- Changes require 5-of-7 signatures + 90-day review
- Community can propose improvements

#### Defense Against Capture

Formal verification makes Bitcoin governance **6x harder to capture**:

1. **Technical Barrier**: Must bypass automated verification
2. **Social Barrier**: Must convince 6-of-7 maintainers
3. **Time Barrier**: 180-365 day review periods
4. **Transparency Barrier**: All verification results public
5. **Audit Barrier**: OpenTimestamps immutable proof
6. **Community Barrier**: Public review + economic node veto

**Key Insight**: An attacker cannot simply "convince maintainers" - they must also produce mathematically correct code that passes verification. This dramatically raises the bar for malicious changes.

#### Verification Status

Current verification coverage: [Link to docs/VERIFICATION.md]

See [Cross-Layer Dependencies](architecture/CROSS_LAYER_DEPENDENCIES.md) for separation rules.

### Meta-Governance

Changes to governance rules themselves require:
- 5-of-7 maintainers + 2-of-3 emergency keyholders
- 90-day review period
- 30-day public comment period
- Rationale document required

### Maintainer Lifecycle

**Adding Maintainers:**
- Nominated by existing maintainer
- 5-of-7 approval from current maintainers
- 30-day community comment period
- Must demonstrate technical competence and alignment with Bitcoin principles

**Contributor Progression:**
See [CONTRIBUTOR_GUIDE.md](CONTRIBUTOR_GUIDE.md) for possible paths from contributor to maintainer. These are documented options, not rigid requirements. Merit-based selection emerges naturally through contributions.

**Removing Maintainers:**
- 6-of-7 vote (excluding subject maintainer)
- Formal warning logged in `warnings/` directory
- 14-day notice period
- Reasons: inactivity (6+ months), code of conduct violations **on-platform only** (off-platform activity disregarded), competence concerns

**Rotation:**
- Maintainers may voluntarily step down with 30-day notice
- Encouraged rotation every 3-5 years to prevent centralization
- Emeritus status available for advisory role

### Ostrom Principles Compliance

BTCDecoded governance follows Elinor Ostrom's principles for managing common-pool resources:

1. **Clearly Defined Boundaries**: Maintainer roles and repository scope defined
2. **Proportional Equivalence**: Higher-layer (constitutional) changes require more consensus
3. **Collective Choice**: Maintainers participate in rule-making that affects them
4. **Monitoring**: Governance App enforces rules transparently on GitHub
5. **Graduated Sanctions**: Warning system before maintainer removal
6. **Conflict Resolution**: Meta-governance process for disputes
7. **Minimal Recognition of Rights**: GitHub org recognizes this governance structure
8. **Nested Enterprises**: Layered architecture with appropriate rules per layer

**Note:** We govern the *codebase commons* (repository access), not the *network commons* (Bitcoin protocol). Users govern the network through voluntary adoption.



