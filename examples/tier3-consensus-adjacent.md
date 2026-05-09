# Example: Tier 3 consensus-adjacent PR

This document outlines how a **Tier 3** (consensus-adjacent) change differs from routine work. These PRs touch validation, serialization, or behavior that could affect chain consensus if mis-applied.

## Scenario

A change adjusts transaction validation in a way that must remain compatible with the network’s consensus rules (e.g., tightening checks that nodes already perform, or fixing a spec bug with a coordinated rollout).

## Expected flow (illustrative)

1. **Design and rationale** published early (issue or RFC-style discussion).
2. **Broader review**: more reviewers, longer soak time, and explicit compatibility notes.
3. **Test plan**: unit tests, integration tests, and optional testnet / staging verification.
4. **Attestations** per governance rules; often **higher thresholds** than Tier 1–2.
5. **Deployment** may require flags, version gates, or migration steps documented in the PR.

## Notes

- Follow [consensus-change-workflow.md](./consensus-change-workflow.md) for end-to-end consensus governance.
- For urgent security fixes, see [emergency-response.md](./emergency-response.md).
