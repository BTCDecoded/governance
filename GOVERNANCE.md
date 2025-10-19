# BTCDecoded Governance Process

## How Governance Works

### Pull Request Process

1. Developer opens PR
2. Governance App validates requirements
3. Maintainers review and sign: `/governance-sign <signature>`
4. Review period elapses
5. Requirements met → merge enabled
6. PR merged

### Signature Requirements by Layer

- **Layer 1-2 (Constitutional)**: 6-of-7 maintainers, 180 days
- **Layer 3 (Implementation)**: 4-of-5 maintainers, 90 days
- **Layer 4 (Application)**: 3-of-5 maintainers, 60 days
- **Layer 5 (Extension)**: 2-of-3 maintainers, 14 days

### Emergency Tier System

BTCDecoded uses a three-tiered emergency response system for proportional handling of critical issues.

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

**Removing Maintainers:**
- 6-of-7 vote (excluding subject maintainer)
- Formal warning logged in `warnings/` directory
- 14-day notice period
- Reasons: inactivity (6+ months), misconduct, competence concerns

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



