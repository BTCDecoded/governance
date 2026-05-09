# Cross-layer dependencies

Bitcoin Commons is organized in layers (consensus, protocol, node, SDK, governance tooling). Changes in one layer often constrain or require updates in others.

## Principles

- **Consensus immutability**: consensus code paths are the highest-risk surface; dependents must not weaken or diverge from specified behavior without an explicit governance-backed change process.
- **Explicit interfaces**: protocol and node layers should expose stable, documented boundaries so governance and tooling can reason about compatibility.
- **Order of rollout**: upgrades that affect wire format or validation typically require coordinated releases (libraries, nodes, optional apps).

## Typical dependency graph (logical)

```text
consensus → protocol → node → SDK / applications → governance enforcement
```

Not every change propagates through all layers; the graph is a guideline for impact analysis.

## When changing code

- Identify **which tier** the change falls under in your governance model.
- List **consumers**: crates, binaries, and external integrations affected.
- Plan **verification**: tests, compatibility matrices, and monitoring for the rollout.

For cryptographic governance basics, see [CRYPTOGRAPHIC_GOVERNANCE.md](./CRYPTOGRAPHIC_GOVERNANCE.md). For fork semantics, see [GOVERNANCE_FORK.md](./GOVERNANCE_FORK.md).
