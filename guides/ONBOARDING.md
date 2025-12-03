# Onboarding Guide

**Purpose**: Structured path for onboarding new maintainers and contributors  
**Audience**: New maintainers, contributors, potential successors

## Prerequisites

| Category | Requirements |
|----------|-------------|
| **Essential** | Rust programming (intermediate+), Git/GitHub workflow, command-line proficiency (Linux/macOS) |
| **Highly Recommended** | Bitcoin protocol knowledge, cryptography basics (ECDSA, hashing), formal verification concepts, software architecture |
| **Nice to Have** | Bitcoin Core codebase experience, model checking/formal verification experience, governance system experience |

**Knowledge Base**: Bitcoin consensus rules (high level), BIPs, how nodes validate blocks/transactions, basic cryptography (signatures, hashing).

## Week 1: Foundation

| Days | Focus | Tasks | Deliverable |
|------|-------|-------|-------------|
| **1-2** | Project Overview | Read `README.md`, `governance/GOVERNANCE.md`, `governance/SUCCESSION_PLAN.md`, browse repo structure, read `blvm-consensus/README.md` | 1-page project summary |
| **3-4** | blvm-spec | Read `blvm-spec/THE_ORANGE_PAPER.md` (sections 1-5), review mathematical notation, understand state transitions | Notes on Orange Paper structure and key rules |
| **5-7** | Consensus Implementation | Read `blvm-consensus/src/block.rs`, `transaction.rs`, `bip_validation.rs`, trace block validation, run tests | Diagram of block validation flow |

## Week 2: Deep Dive

| Days | Focus | Tasks | Deliverable |
|------|-------|-------|-------------|
| **8-10** | Script Execution | Read `blvm-consensus/src/script.rs`, understand `verify_script()` and `verify_signature()`, review BIP integration points, run script tests | Notes on script execution flow and BIP integration gaps |
| **11-12** | Formal Verification | Read `blvm-consensus/docs/CONSENSUS_COVERAGE_ASSESSMENT.md`, review Kani proof example, run Kani (if installed), understand proof limitations | Summary of verification coverage and gaps |
| **13-14** | Testing | Review `blvm-consensus/tests/` structure, run all tests, review integration/property-based tests, understand 6-layer verification system | Test coverage summary |

## Week 3: Governance and Operations

| Days | Focus | Tasks | Deliverable |
|------|-------|-------|-------------|
| **15-17** | Governance System | Read `governance/GOVERNANCE.md`, review `governance/config/`, read `governance/examples/emergency-response.md`, understand tier classification and signature requirements | Governance process flowchart |
| **18-19** | Governance App | Review `blvm-commons/` structure, understand governance enforcement, review database schema, understand status checks and audit logging | Architecture diagram of governance app |
| **20-21** | First Contribution | Find small non-critical issue, make fix (documentation/test/bug), open PR, go through review, get PR merged | First merged PR |

## First Tasks (Non-Critical)

| Category | Tasks |
|----------|-------|
| **Documentation** | Improve code comments, update README files, fix documentation typos |
| **Testing** | Add edge case tests, improve test coverage, add debug assertions |
| **Code Quality** | Refactor non-critical code, improve error messages, add debug tools |

## Mentorship Plan

| Scenario | Approach |
|----------|----------|
| **Primary Maintainer Available** | Week 1-2: Daily check-ins, Q&A, code walkthroughs. Week 3-4: Pair programming, code review, gradual handoff. Ongoing: Weekly sync, code review participation |
| **Primary Maintainer Unavailable** | Follow onboarding guide, use succession plan, review commit history, study test cases. Start small (documentation, tests, non-critical bugs). Build knowledge incrementally |

## Common Pitfalls

| Pitfall | Problem | Solution |
|---------|---------|----------|
| **Trying to understand everything at once** | Overwhelming information | Follow week-by-week plan, focus on one area |
| **Making changes too early** | Breaking consensus-critical code | Start with documentation and tests |
| **Ignoring governance** | PRs rejected due to violations | Understand governance before making changes |
| **Not understanding dependencies** | Breaking layer dependencies | Understand 5-tier architecture first |
| **Skipping tests** | Introducing bugs | Always add tests, run existing tests |

## Success Metrics

| Timeline | Metrics |
|----------|---------|
| **After Week 1** | Can explain project purpose/architecture, understands governance, has read Orange Paper overview |
| **After Week 2** | Can trace block validation flow, understands script execution, knows where BIP checks happen |
| **After Week 3** | Understands governance process, has made first contribution, can open/manage PRs |
| **After Month 1** | Can make non-critical changes independently, understands consensus code structure, can review PRs |
| **After Month 3** | Can make consensus-adjacent changes (with review), understands formal verification, can maintain Kani proofs |

## Resources

| Category | Resources |
|----------|-----------|
| **Internal** | [Succession Plan](../SUCCESSION_PLAN.md), [Governance Guide](../GOVERNANCE.md), [Maintainer Guide](./MAINTAINER_GUIDE.md), [Emergency Response](../examples/emergency-response.md) |
| **External** | [Bitcoin Core Documentation](https://bitcoin.org/en/developer-documentation), [BIPs](https://github.com/bitcoin/bips), [Rust Book](https://doc.rust-lang.org/book/), [Kani Documentation](https://model-checking.github.io/kani/) |

## Next Steps

After completing onboarding:
1. Continue learning (study Bitcoin Core, read BIPs, learn formal verification)
2. Contribute regularly (fix bugs, improve documentation, add tests)
3. Build expertise (focus on one area, become go-to person, mentor others)
4. Prepare for maintainership (demonstrate reliability, show deep understanding, contribute to critical areas)
