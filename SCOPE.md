# BTCDecoded Governance Scope

## Executive Summary

BTCDecoded governance is **binding** for repository access and **advisory** for protocol changes. Maintainers control what enters the official codebase, but users control what runs on the network.

This document clarifies the distinction between repository governance (what we control) and protocol governance (what we don't control).

## Domain 1: Repository Governance (Binding)

### What We Control

**Merge Access:**
- Who can commit code to BTCDecoded repositories
- When pull requests can be merged
- What code quality standards apply
- Release timing and versioning

**Maintainer Management:**
- Selection and removal of maintainers
- Maintainer roles and responsibilities
- Access permissions
- Emeritus status

**Release Creation:**
- Official BTCDecoded release builds
- Release notes and documentation
- Distribution via BTCDecoded channels
- Version numbering

**Code Quality:**
- Test coverage requirements
- Documentation standards
- Code review processes
- CI/CD enforcement

### Authority Scope

These decisions are **binding within the BTCDecoded GitHub organization**. Maintainer signatures required for merge are enforced by the Governance App via GitHub status checks.

### Mechanism

Multi-signature governance with layer-appropriate thresholds:
- Constitutional layers (1-2): 6-of-7 maintainers
- Implementation layer (3): 4-of-5 maintainers
- Application layer (4): 3-of-5 maintainers
- Extension layer (5): 2-of-3 maintainers

## Domain 2: Protocol Governance (Advisory)

### What We Don't Control

**Bitcoin Network Consensus:**
- Consensus rule changes
- Block validation logic
- Transaction acceptance criteria
- Network protocol rules

**User Adoption:**
- Whether users run BTCDecoded software
- Which version users choose to run
- Whether users upgrade
- Whether users fork the code

**Node Operator Choices:**
- Configuration decisions
- Network participation
- Software alternatives
- Policy settings

**Miner Signaling:**
- Hash power allocation
- Version bit signaling
- Block template selection
- Fee policies

### Authority Scope

BTCDecoded maintainers have **zero enforcement power** over the Bitcoin network. We can approve code for release, but we cannot force adoption.

### Mechanism

**Voluntary Adoption:**

1. **Maintainers Approve**: 6-of-7 signatures on consensus-affecting code
2. **Code Released**: Published as optional upgrade
3. **Users Decide**: Node operators choose whether to upgrade
4. **Network Signals**: Version bits, node counts, economic activity
5. **Activation**: Based on user signaling thresholds (if applicable)

**Key Principle:** No amount of maintainer signatures forces network adoption. Users retain complete sovereignty.

## Relationship Between Domains

### How They Interact

```
Repository Governance → Code Approval → Release
                                          ↓
                              User Choice (Advisory)
                                          ↓
                              Network Adoption (or Not)
```

**Repository governance enables release. User choice determines adoption.**

### Consensus Change Example

Suppose maintainers approve a consensus rule change:

**Repository Side (Binding):**
- PR requires 6-of-7 maintainer signatures ✓
- 365-day review period must elapse ✓
- BIP specification must exist ✓
- Test vectors must be comprehensive ✓
- Security audit must pass ✓
- Equivalence proof must be valid ✓

**Network Side (Advisory):**
- Code released as optional upgrade
- Users choose whether to run it
- Network signaling measured (75% nodes, 90% hash power, economic majority)
- Activation decision based on actual adoption
- **Users can reject regardless of maintainer consensus**

### What Happens If Users Reject

If 6-of-7 maintainers approve a consensus change but users don't adopt:

1. **Code enters repository** (repository governance binding)
2. **Release published** (repository governance binding)
3. **Network ignores it** (user sovereignty)
4. **Change doesn't activate** (protocol governance advisory)

Result: Maintainers approved code that users rejected. Users remain sovereign.

## User Sovereignty Guarantee

### Rights Users Always Retain

**Right to Fork:**
- Users can fork BTCDecoded code at any time
- Users can fork Bitcoin itself if dissatisfied
- No maintainer approval required
- No governance process can prevent forks

**Right to Run Alternatives:**
- Users can run Bitcoin Core, btcd, bcoin, or any implementation
- No obligation to use BTCDecoded software
- Can mix and match implementations
- Can write new implementations

**Right to Reject Changes:**
- Users can refuse to upgrade
- Users can run older versions indefinitely
- No forced upgrades possible
- Network consensus determined by economic majority

**Right to Propose Alternatives:**
- Users can submit competing BIPs
- Users can implement and release alternatives
- Users can advocate for different approaches
- Community discussion remains open

### Historical Context: Bitcoin Governance

**Bitcoin Core Precedent:**
- Bitcoin Core has no formal governance
- Maintainers have commit access
- Consensus changes require broad community support
- Users have repeatedly rejected Core proposals (e.g., SegWit2x)

**Key Historical Events:**

1. **SegWit2x (2017)**: Major companies and miners supported. Users rejected. Proposal cancelled.
2. **UASF (2017)**: Users threatened fork to activate SegWit. Miners complied with user demand.
3. **Block Size Debate (2015-2017)**: Years of debate, multiple forks (BCH, BSV), demonstrated user sovereignty.

**Lesson:** Bitcoin users govern the protocol through voluntary coordination. No centralized authority can force changes.

### BTCDecoded Position

We adopt Bitcoin's user sovereignty model:

- **Repository governance provides structure** (managing the commons)
- **Protocol governance remains emergent** (user coordination)
- **Maintainers propose, users dispose** (advisory nature)
- **Economic majority decides** (market forces)

## Ostrom Principles Compliance

Elinor Ostrom's principles for managing common-pool resources apply to **repository governance** (the codebase), not **protocol governance** (the network).

### Codebase as Common-Pool Resource

**Resource:** BTCDecoded GitHub repositories and commit access

**Governance Application:**

1. **Clearly Defined Boundaries**: Maintainers defined, repository scope explicit
2. **Proportional Equivalence**: Higher layers require more consensus (6-of-7 vs 2-of-3)
3. **Collective Choice**: Maintainers participate in governance rule-making
4. **Monitoring**: Governance App enforces rules transparently
5. **Graduated Sanctions**: Warning system before maintainer removal
6. **Conflict Resolution**: Meta-governance process for disputes
7. **Minimal Recognition of Rights**: GitHub recognizes governance structure
8. **Nested Enterprises**: Layered architecture with tier-appropriate rules

**Ostrom Compliance:** We govern access to the **codebase commons**, not the **network commons**.

### Network as Separate Commons

**Resource:** Bitcoin network consensus rules

**Governance Reality:**
- No formal governance structure
- Emergent coordination among users
- Economic incentives drive behavior
- Fork mechanism for disputes
- User sovereignty paramount

**Ostrom Limitation:** Ostrom's principles apply to managed commons with defined boundaries. Bitcoin's network has no central authority to manage it. Users self-organize.

**BTCDecoded Approach:** We don't claim to govern the network. We govern our repositories and make advisory recommendations.

## Comparison to Other Projects

### Bitcoin Core

**Repository Governance:**
- Informal, no signature requirements
- Maintainers have commit access
- Review-based (ACK/NACK)
- No enforcement mechanism

**Protocol Governance:**
- Advisory only
- Community consensus required
- Users retain sovereignty
- Historical precedent strong

### Ethereum

**Repository Governance:**
- Core dev teams maintain implementations
- Informal process
- No signature requirements

**Protocol Governance:**
- Core devs coordinate hard forks
- EIP process for proposals
- Community signaling (coin votes, social consensus)
- More frequent changes than Bitcoin

### BTCDecoded

**Repository Governance:**
- Formal multi-signature requirements
- Enforcement via Governance App
- Layer-appropriate thresholds
- Transparent and auditable

**Protocol Governance:**
- Advisory only (like Bitcoin Core)
- User sovereignty explicit
- Formal signaling thresholds recommended
- Longer review periods (365 days for consensus)

**Innovation:** We formalize repository governance while maintaining advisory-only protocol governance.

## Practical Implications

### For Maintainers

**You Control:**
- What enters BTCDecoded repositories
- When releases are published
- Code quality standards
- Development priorities

**You Don't Control:**
- Whether users adopt your code
- Bitcoin network consensus rules
- User configuration choices
- Alternative implementations

**Your Role:**
- Steward the codebase
- Review and approve quality code
- Coordinate releases
- Advocate for good protocol design
- **Serve users, don't command them**

### For Users

**You Control:**
- Whether to run BTCDecoded software
- Which version to run
- Whether to upgrade
- Whether to fork and modify
- Bitcoin consensus rules (via economic coordination)

**You Don't Control:**
- What enters BTCDecoded repositories (unless you're a maintainer)
- What maintainers choose to work on
- Release timing

**Your Role:**
- Choose software that serves your needs
- Signal preferences through adoption
- Participate in protocol discussions
- Fork if dissatisfied
- **Exercise sovereignty responsibly**

### For the Ecosystem

**Healthy Dynamics:**
- Maintainers propose quality changes
- Users evaluate and choose
- Economic incentives align
- Forks possible but rare
- Coordination without coercion

**Unhealthy Dynamics to Avoid:**
- Maintainers claiming protocol authority
- Users expecting maintainers to "fix" the network
- Confusion between repository and protocol governance
- Centralization of decision-making
- Forced upgrades

## Conclusion

BTCDecoded governance is **dual-track**:

1. **Repository Governance (Binding)**: Multi-signature control over merge access and releases
2. **Protocol Governance (Advisory)**: User sovereignty over network adoption

We formalize what we control (repositories) and explicitly disclaim what we don't (the network).

This approach:
- Provides structure for codebase management
- Preserves user sovereignty for protocol changes
- Follows Ostrom's principles for the codebase commons
- Respects Bitcoin's ethos of decentralization
- Makes our authority explicit and limited

**Maintainers serve users. Users govern Bitcoin.**

---

*For questions about this scope distinction, see GOVERNANCE.md or open a discussion in the governance repository.*


