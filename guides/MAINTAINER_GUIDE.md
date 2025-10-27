# Maintainer Guide

Guide for maintainers on how to use the BTCDecoded governance system.

## ⚠️ IMPORTANT: Phase 1 Status

**This system is currently UNRELEASED and UNTESTED in production.**

- ✅ **Infrastructure Complete**: All core components implemented
- ⚠️ **Not Yet Activated**: Governance rules are not enforced
- 🔧 **Test Keys Only**: No real cryptographic enforcement
- 📋 **Development Phase**: System is in rapid AI-assisted development

## Overview

This guide explains how maintainers will interact with the governance system once it's activated in Phase 2. Currently, the system is in development and uses test keys only.

## Key Management

### Generating Real Keys (Phase 2+)

**⚠️ DO NOT GENERATE REAL KEYS UNTIL PHASE 2 ACTIVATION**

When Phase 2 is activated, maintainers will need to generate real cryptographic keys:

```bash
# Generate new keypair using developer-sdk
cargo run --bin generate-keypair -- --output maintainer-keys.json

# This will create:
# - maintainer-keys.json (private key - keep secure)
# - maintainer-keys.pub (public key - share with governance system)
```

### Key Security

- **Private Key**: Store securely, never share
- **Public Key**: Share with governance system administrators
- **Backup**: Create secure backups of private keys
- **Rotation**: Plan for key rotation procedures

### Key Format

Keys are generated in the following format:

```json
{
  "private_key": "hex-encoded-private-key",
  "public_key": "hex-encoded-public-key",
  "key_id": "unique-key-identifier",
  "created_at": "2024-01-01T00:00:00Z"
}
```

## Signature Process

### How to Sign PRs

Once the system is activated, maintainers will sign PRs using the developer-sdk CLI:

```bash
# Sign a PR (Phase 2+)
cargo run --bin sign-pr -- --pr 123 --message "I approve this change"

# This will:
# 1. Generate a signature for the PR
# 2. Post a comment with the signature
# 3. Update the governance status
```

### Signature Format

Signatures are posted as GitHub comments in the following format:

```
/governance-sign <signature>
```

Where `<signature>` is a hex-encoded cryptographic signature.

### Signature Verification

The governance system will:

1. **Extract Signature**: Parse the signature from the comment
2. **Verify Signature**: Cryptographically verify the signature
3. **Check Maintainer**: Verify the signer is an authorized maintainer
4. **Update Status**: Update the PR's governance status
5. **Log Event**: Record the signature in the audit log

## PR Classification

### Automatic Classification

The system automatically classifies PRs into tiers based on:

- **File Changes**: Which files are modified
- **PR Title**: Keywords in the title
- **PR Body**: Content and labels
- **Repository**: Which repository the PR is in

### Manual Override

Maintainers can manually override the classification:

```bash
# Override PR classification (Phase 2+)
cargo run --bin override-tier -- --pr 123 --tier 4 --rationale "Emergency security fix"
```

### Tier Requirements

Each tier has different signature requirements:

- **Tier 1 (Routine)**: 3-of-5 signatures, 7 days
- **Tier 2 (Feature)**: 4-of-5 signatures, 30 days
- **Tier 3 (Consensus-Adjacent)**: 5-of-5 signatures, 90 days + economic node veto
- **Tier 4 (Emergency)**: 4-of-5 signatures, 24 hours
- **Tier 5 (Governance)**: 5-of-5 signatures, 180 days

## Emergency Procedures

### Emergency Activation

For Tier 4 (Emergency) PRs:

1. **Immediate Classification**: PR is automatically classified as Tier 4
2. **Notification**: All maintainers are notified immediately
3. **Signature Collection**: 4-of-5 signatures required within 24 hours
4. **Economic Node Oversight**: Economic nodes are notified for oversight
5. **Post-Mortem**: Required within 30 days of activation

### Emergency Extension

Emergency activations can be extended if needed:

```bash
# Extend emergency (Phase 2+)
cargo run --bin extend-emergency -- --pr 123 --days 7 --rationale "Additional time needed"
```

### Emergency Deactivation

Emergency can be deactivated if no longer needed:

```bash
# Deactivate emergency (Phase 2+)
cargo run --bin deactivate-emergency -- --pr 123 --rationale "Issue resolved"
```

## Economic Node Interaction

### Veto Signals

Economic nodes can submit veto signals for Tier 3+ PRs:

- **Veto**: Block the PR from merging
- **Support**: Support the PR
- **Abstain**: Neutral position

### Veto Thresholds

- **Mining Veto**: 30%+ hashpower veto
- **Economic Veto**: 40%+ economic activity veto
- **Combined**: Either threshold can block the PR

### Veto Response

If a veto is active:

1. **PR Blocked**: Merge is automatically blocked
2. **Status Updated**: GitHub status shows veto active
3. **Notification**: Maintainers are notified
4. **Resolution**: PR cannot merge until veto is resolved

## Governance Changes

### Tier 5 Process

Governance changes (Tier 5) require:

1. **Extended Review**: 180-day review period
2. **Economic Node Signaling**: 50%+ hashpower, 60%+ economic activity
3. **Special Process**: Additional requirements and oversight
4. **Fork Capability**: Nodes can choose different governance rulesets

### Governance Fork

If governance changes are controversial:

1. **Export Configuration**: Current governance config is exported
2. **Node Decisions**: Economic nodes choose which ruleset to follow
3. **Adoption Tracking**: System tracks adoption of different rulesets
4. **Fork Resolution**: Eventually one ruleset becomes dominant

## Monitoring and Alerts

### Status Monitoring

Maintainers can monitor governance status:

```bash
# Check PR status (Phase 2+)
cargo run --bin check-status -- --pr 123

# Check system status
cargo run --bin system-status
```

### Alerts

The system will send alerts for:

- **Signature Requirements**: When signatures are needed
- **Time Windows**: When review periods are expiring
- **Veto Signals**: When economic nodes submit vetoes
- **System Issues**: When the governance system has problems

## Best Practices

### For Maintainers

1. **Stay Informed**: Monitor governance status regularly
2. **Respond Quickly**: Sign PRs promptly when requirements are met
3. **Understand Tiers**: Know the requirements for each tier
4. **Communicate**: Coordinate with other maintainers
5. **Document**: Provide clear rationale for decisions

### For PR Authors

1. **Classify Correctly**: Use appropriate labels and titles
2. **Provide Context**: Explain the changes and rationale
3. **Be Patient**: Respect the governance process
4. **Engage**: Respond to maintainer questions
5. **Follow Process**: Don't try to bypass governance

## Troubleshooting

### Common Issues

1. **Signature Not Recognized**: Check key format and permissions
2. **PR Not Classified**: Verify file changes and content
3. **Status Not Updating**: Check webhook delivery and permissions
4. **Veto Not Clearing**: Verify economic node signals

### Debug Commands

```bash
# Debug PR classification
cargo run --bin debug-classification -- --pr 123

# Debug signature verification
cargo run --bin debug-signature -- --signature <signature>

# Debug veto status
cargo run --bin debug-veto -- --pr 123
```

### Getting Help

1. **Check Documentation**: Review this guide and other docs
2. **Ask Questions**: Use GitHub discussions
3. **Report Issues**: Use GitHub issues for bugs
4. **Community**: Engage with the development community

## Security Considerations

### Key Security

- **Never Share Private Keys**: Keep private keys secure
- **Use Secure Storage**: Store keys in secure locations
- **Regular Rotation**: Plan for key rotation
- **Backup Safely**: Create secure backups

### Signature Security

- **Verify Context**: Ensure you're signing the right PR
- **Check Content**: Review PR content before signing
- **Understand Impact**: Know what the PR changes
- **Coordinate**: Work with other maintainers

### System Security

- **Trust the System**: The governance system is designed to be secure
- **Report Issues**: Report any security concerns
- **Stay Updated**: Keep up with system updates
- **Follow Procedures**: Use established procedures

## Future Developments

### Phase 2 Features

- **Real Enforcement**: Actual governance enforcement
- **Production Keys**: Real cryptographic keys
- **Security Audit**: Completed security audit
- **Community Validation**: Community-tested system

### Phase 3 Features

- **Mature System**: Battle-tested in production
- **Advanced Features**: Additional governance capabilities
- **Integration**: Better integration with Bitcoin ecosystem
- **Community**: Full community adoption

## Contact and Support

### Development Team

- **GitHub Issues**: Report bugs and feature requests
- **GitHub Discussions**: Ask questions and provide feedback
- **Pull Requests**: Contribute code and improvements

### Security

- **Security Issues**: Report privately to maintainers
- **Vulnerabilities**: Follow responsible disclosure
- **Audit Results**: Will be published when available

## ⚠️ Final Warning

**This system is currently in development. Do not use real keys or deploy in production until Phase 2 activation.**

---

**Remember**: This system is designed to make Bitcoin governance more transparent, accountable, and resistant to capture. But it's still in development. Stay informed, provide feedback, and wait for the official release.
