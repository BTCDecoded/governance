# Example: Tier 1 routine maintenance PR

This document sketches a **Tier 1** change: low-risk maintenance such as documentation fixes, non-consensus bug fixes, or performance tweaks without protocol impact.

## Scenario

A contributor opens a PR that updates error messages and adds regression tests. No consensus rules, wire format, or validation logic changes.

## Expected flow (illustrative)

1. **Open PR** with a clear description linking to the issue or rationale.
2. **Required reviewers** per your repo’s ruleset (e.g., one maintainer for Tier 1).
3. **Signatures / attestations** as required by the active governance ruleset (see [consensus-change-workflow.md](./consensus-change-workflow.md) for higher tiers).
4. **Merge** once checks and policy gates pass.

## Notes

- Exact thresholds and tiers are defined in your repository’s governance configuration, not in this stub.
- For consensus-adjacent or emergency paths, see [tier3-consensus-adjacent.md](./tier3-consensus-adjacent.md) and [emergency-response.md](./emergency-response.md).
