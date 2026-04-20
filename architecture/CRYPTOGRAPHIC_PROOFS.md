# Cryptographic proofs in governance

## Scope

This repository’s **enforced** governance proofs are about **maintainer identity and intent on PRs**: signatures over agreed messages, auditability, and (where deployed) hash chains and timestamps.

There is **no** separate registry that auto-activates “nodes” from holdings or exchange proofs for merge control.

## Maintainer PR signatures

- Maintainers sign approval of specific PR content and metadata.
- Verification lives in the commons webhook and validation stack (e.g. `blvm-commons/src/validation/signatures.rs`, comment handlers under `blvm-commons/src/webhooks/`).

Use the [Maintainer Guide](../guides/MAINTAINER_GUIDE.md) for the operational signing flow.

## Ruleset integrity

Exported governance rulesets (when used) should be **hashable and signable** so users can pin a configuration. See [Governance Fork](./GOVERNANCE_FORK.md) for packaging and verification concepts.

## Summary

| Area | Role |
|------|------|
| Maintainer signatures | Authorize merges under tier/layer policy |
| Audit / timestamps | Tamper-evidence for governance events (where enabled) |
| Contribution analytics | Optional; not a merge gate by default |
