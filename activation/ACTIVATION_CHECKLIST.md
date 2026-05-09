# Activation checklist

This is a short, actionable checklist for moving the BTCDecoded governance system from infrastructure-only to enforced operation. Expand with repository-specific steps as your deployment solidifies.

## Before enforcement

- [ ] Security review or audit completed for the enforcement stack you run in production.
- [ ] Production keys generated, stored, and access-controlled (see maintainer and key-management docs).
- [ ] GitHub App (or equivalent) credentials, webhooks, and required secrets configured in a secrets manager.
- [ ] Database backups, restore drills, and monitoring alerts in place.

## Rollout

- [ ] Run a dry-run period: log enforcement decisions without blocking merges.
- [ ] Define escalation paths for false positives and emergency bypass (document who can act and how it is logged).
- [ ] Communicate the activation timeline to all affected maintainers and repositories.

## Post–go-live

- [ ] Review enforcement logs weekly for the first month.
- [ ] Track metrics (latency, error rate, contested PRs) and adjust thresholds as needed.

For the phased plan, see [PHASE_ACTIVATION.md](./PHASE_ACTIVATION.md).
