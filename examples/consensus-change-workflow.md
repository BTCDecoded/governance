# Consensus Change Workflow

Step-by-step guide for proposing and activating Bitcoin consensus rule changes through BTCDecoded governance.

## Overview

**Critical Distinction:** This workflow governs **repository approval** (what enters BTCDecoded code), not **network adoption** (what Bitcoin runs). Maintainers approve code for release. Users decide whether to run it.

## Phases

### Phase 1: Proposal (Before PR)

**Duration:** Variable (weeks to months of discussion)

**Steps:**

1. **Research and Design**
   - Identify problem or improvement
   - Research existing solutions
   - Design proposed change
   - Consider Bitcoin principles and trade-offs

2. **Community Discussion**
   - Open GitHub Discussion in Orange Paper repo
   - Present problem and proposed solution
   - Engage with community feedback
   - Iterate on design

3. **Write BIP Specification**
   - Draft Bitcoin Improvement Proposal
   - Include motivation, specification, rationale
   - Reference existing standards (BIP2)
   - Submit to bitcoin-dev mailing list

4. **Create Test Vectors**
   - Develop comprehensive test cases
   - Include edge cases and error conditions
   - Provide reference implementations
   - Document expected behavior

5. **Write Equivalence Proof**
   - Prove mathematical correctness (for Consensus Proof layer)
   - Demonstrate equivalence with specification
   - Use formal methods where applicable
   - Review by cryptographers/mathematicians

6. **Security Audit Planning**
   - Identify qualified auditors
   - Define scope of audit
   - Budget and timeline
   - Disclosure plan

### Phase 2: Pull Request (Repository Approval)

**Duration:** 365 days minimum (1 year review period)

**Requirements (Binding):**
- 6-of-7 maintainer signatures
- 365-day review period
- BIP specification approved
- Test vectors comprehensive
- Security audit passed
- Equivalence proof validated

**Steps:**

1. **Open Pull Request**
   - Target: `orange-paper` or `consensus-proof` repository
   - Title: `[CONSENSUS] BIP-XXX: <description>`
   - Link to BIP, tests, proof, audit
   - Clear rationale and implementation notes

2. **Governance App Validation**
   - App detects consensus rule change (path patterns)
   - Applies 365-day review period
   - Requires 6-of-7 maintainer threshold
   - Checks for required artifacts

3. **Technical Review (Ongoing)**
   - Maintainers review code quality
   - Verify test coverage
   - Check specification adherence
   - Assess security implications
   - Review equivalence proof

4. **Community Review (Public)**
   - Open to all developers and users
   - Comments on GitHub PR
   - Discussion on mailing lists
   - Independent implementations encouraged

5. **Security Audit (Required)**
   - Professional security firm review
   - Vulnerability assessment
   - Report published (timing depends on findings)
   - Issues addressed before merge

6. **Maintainer Signatures**
   - Each maintainer signs when satisfied
   - Command: `/governance-sign <signature>`
   - Signature includes PR hash, BIP number, timestamp
   - Cryptographically verified by Governance App

7. **Review Period Elapses**
   - 365 days from PR opening
   - Cannot be shortened (even with emergency mode)
   - Ensures thorough vetting
   - Allows ecosystem preparation

8. **Merge Enabled**
   - All requirements met (signatures + time)
   - Governance App enables merge button
   - Lead maintainer merges PR
   - Code enters BTCDecoded repository

**At This Point:** Repository approval complete. Code is officially BTCDecoded consensus rules.

### Phase 3: Release (Optional Upgrade Available)

**Duration:** Variable

**Steps:**

1. **Integration Testing**
   - Merge into reference node implementation
   - Test with real-world scenarios
   - Verify backward compatibility
   - Document migration path

2. **Release Build**
   - Compile binaries for all platforms
   - Create release notes
   - Document new consensus rules
   - Highlight upgrade requirements

3. **Release Announcement**
   - Publish on BTCDecoded website
   - Post to bitcoin-dev mailing list
   - Social media and community channels
   - Clear explanation of changes

4. **Optional Upgrade Available**
   - Users can download new version
   - No forced upgrades
   - Old versions remain available
   - Users make informed choice

**At This Point:** Code is available. Users begin evaluating.

### Phase 4: User Signaling (Advisory)

**Duration:** 90+ days (measurement period)

**Nature:** Advisory, not mandatory. Maintainers cannot force adoption.

**Steps:**

1. **Node Operators Evaluate**
   - Review BIP specification
   - Read security audit
   - Test in development environments
   - Assess risks and benefits

2. **Voluntary Upgrade**
   - Node operators choose to upgrade (or not)
   - Each operator makes independent decision
   - Economic incentives influence choice
   - Network effects emerge

3. **Signaling Measurement**
   - **Method:** BIP9-style version bits or node polling
   - **Metrics:**
     - Node adoption: % running new version
     - Hash power signaling: % of blocks signaling support
     - Economic activity: Exchange and major wallet adoption
   
4. **Threshold Monitoring (Recommended)**
   - 75% node adoption
   - 90% hash power signaling
   - Economic majority (e.g., 5 of top 10 exchanges)
   
   **Note:** These are recommended thresholds for maintainers to consider a change "widely supported." They do not trigger automatic activation.

5. **Community Discussion**
   - Ongoing debate about adoption
   - User feedback on implementation
   - Bug reports addressed
   - Coordination among stakeholders

**At This Point:** Network signaling indicates support level. Users remain in control.

### Phase 5: Activation Decision (User Sovereignty)

**Duration:** Variable

**Nature:** Users decide, not maintainers.

**Possible Outcomes:**

#### Outcome A: Soft Fork with User Coordination

1. **Sufficient Support Emerges**
   - Thresholds reached or exceeded
   - Economic majority supports change
   - Miners signal readiness

2. **Activation Method**
   - BIP9 (miner-activated)
   - BIP8 (user-activated with miner signaling)
   - UASF (user-activated soft fork)
   - Choice depends on community preference

3. **Activation Date Set**
   - Coordinated by community (not maintainers)
   - Sufficient lead time for remaining nodes
   - Clear communication of timeline

4. **Network Upgrades**
   - Consensus rules change network-wide
   - Non-upgraded nodes see subset of valid blocks
   - Backward compatible (soft fork)

#### Outcome B: Hard Fork (Permanent Split Possible)

1. **Contentious Change**
   - No clear economic majority
   - Significant opposition exists
   - Competing visions of Bitcoin

2. **Fork Decision**
   - Users choose which chain to support
   - Markets decide which fork has value
   - Both chains may survive
   - Example: Bitcoin vs Bitcoin Cash (2017)

3. **Network Splits**
   - Two incompatible rulesets
   - Two separate blockchains
   - Two separate currencies
   - Users hold coins on both

#### Outcome C: Rejection

1. **Insufficient Support**
   - Users don't upgrade in sufficient numbers
   - Economic majority opposes or ignores
   - Miners don't signal

2. **Change Doesn't Activate**
   - Network continues with old rules
   - Upgraded nodes remain compatible
   - Maintainer-approved code unused by network

3. **Lessons Learned**
   - Community feedback incorporated
   - Revised proposal possible
   - Or idea abandoned

**Key Point:** No amount of maintainer signatures forces adoption. Users govern Bitcoin.

## Example Timeline

**Realistic example for a simple consensus change:**

- **Month 0:** Community discussion begins
- **Month 3:** BIP drafted and submitted
- **Month 6:** Security audit planned
- **Month 9:** Pull request opened (365-day clock starts)
- **Month 12:** Security audit completed
- **Month 15:** Maintainer signatures accumulate
- **Month 21:** All signatures received (6-of-7)
- **Month 21:** 365 days elapsed, merge enabled
- **Month 22:** Merged, integrated into reference node
- **Month 24:** Release published
- **Month 25-27:** User evaluation period
- **Month 28-30:** Node upgrade phase (90-day signaling)
- **Month 33:** Sufficient support achieved
- **Month 36:** Activation date set by community
- **Month 39:** Network-wide activation

**Total:** ~39 months (3.25 years) from discussion to activation

**Why so long?**
- Bitcoin's $2T network cap demands extreme caution
- Consensus changes are permanent and irreversible
- Sufficient time for:
  - Thorough security review
  - Independent implementations
  - Ecosystem preparation
  - User education
  - Coordinated upgrade

## Historical Comparisons

### SegWit (2015-2017)

**Timeline:**
- 2015: BIP141 proposed
- 2016: Soft fork deployed, signaling begins
- 2017: UASF threatened by users
- 2017 August: Activated via user pressure

**Lesson:** Users ultimately decided, despite developer/miner disagreements.

### Taproot (2018-2021)

**Timeline:**
- 2018: Initial proposals
- 2020: BIPs finalized (340, 341, 342)
- 2021: Speedy Trial signaling
- 2021 November: Activated

**Lesson:** Uncontroversial changes activate faster, but still took ~3 years.

### SegWit2x (2017)

**Timeline:**
- 2017: Proposed by major companies and miners
- 2017: Rejected by users and developers
- 2017: Cancelled before activation

**Lesson:** Corporate/miner support insufficient without user buy-in.

## Common Questions

### Q: Can maintainers force a consensus change?

**A:** No. Maintainers control repository merge access, not network adoption. Users run what they choose.

### Q: What if maintainers approve a change users reject?

**A:** The change enters BTCDecoded code but doesn't activate on the network. Unused code.

### Q: What if users want a change maintainers reject?

**A:** Users can fork BTCDecoded, use alternative implementations, or coordinate UASF. User sovereignty preserved.

### Q: Why 365 days for consensus changes?

**A:** Bitcoin's $2T network demands extreme caution. One year allows:
- Thorough security review
- Independent verification
- Ecosystem preparation
- User education
- Identification of unforeseen issues

### Q: Can emergency mode bypass the 365-day review?

**A:** No. Emergency mode doesn't apply to consensus changes. Even Tier 1 critical emergencies maintain signature requirements and have different review timelines. Consensus changes are never "emergency" in the governance sense—they require long timelines by design.

### Q: What about emergency bug fixes in consensus code?

**A:** Critical bugs (inflation, forks) use emergency tiers with shorter review periods (0-30 days) but still require multi-signature approval. These fixes typically restore *intended* consensus rules, not change them.

### Q: How is this different from Bitcoin Core?

**A:** Bitcoin Core has no formal governance. Maintainers merge by informal consensus. BTCDecoded formalizes repository governance with multi-signature requirements but maintains the same advisory-only relationship with the network.

## Best Practices

### For Proposers

1. **Start with discussion, not code**
   - Gauge community interest first
   - Iterate on design before implementation
   - Build consensus informally

2. **Document thoroughly**
   - BIP specification is critical
   - Test vectors prevent implementation divergence
   - Rationale helps future developers

3. **Engage critics**
   - Opposition feedback improves proposals
   - Address concerns genuinely
   - Be willing to adapt or abandon

4. **Think long-term**
   - Consensus changes are permanent
   - 10+ year implications
   - Consider 2nd and 3rd order effects

### For Maintainers

1. **Review rigorously**
   - Consensus changes demand extreme scrutiny
   - Don't rush signatures
   - Consult experts

2. **Communicate clearly**
   - Explain approval decisions
   - Document concerns
   - Maintain transparency

3. **Serve users, not your preferences**
   - Advisory role for network adoption
   - Users govern Bitcoin
   - Humility essential

### For Users

1. **Participate early**
   - Comment on proposals during discussion
   - Test implementations
   - Provide feedback

2. **Evaluate independently**
   - Read BIPs yourself
   - Don't defer to authority
   - Make informed decisions

3. **Exercise sovereignty**
   - Upgrade when you're convinced
   - Don't upgrade out of pressure
   - Fork if necessary

4. **Coordinate carefully**
   - Network effects matter
   - Avoid accidental splits
   - Communication is key

## Conclusion

BTCDecoded governance provides structure for repository management while preserving user sovereignty for protocol changes.

**Repository approval ≠ Network adoption**

This dual-track approach balances the need for quality control (repository governance) with the principle of decentralization (user governance).

Maintainers propose. Users dispose.

---

*For questions or discussion, open an issue in the governance repository.*


