# Security Policy

This document covers repo-specific security boundaries. See the [BTCDecoded Security Policy](https://github.com/BTCDecoded/.github/blob/main/SECURITY.md) for organization-wide policy.

## Supported Versions

| Version | Supported          |
| ------- | ------------------ |
| 0.1.x   | :white_check_mark: |

## Reporting a Vulnerability

**This repository defines governance rules for the entire BTCDecoded ecosystem. Security vulnerabilities in governance configuration could compromise the entire governance system.**

### Critical Security Issues

If you discover a security vulnerability in governance, please report it immediately:

1. **DO NOT** create a public GitHub issue
2. **DO NOT** discuss the vulnerability publicly
3. **DO NOT** post on social media or forums

### How to Report

**Email:** security@btcdecoded.org  
**Subject:** [SECURITY] governance vulnerability

Include the following information:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested fix (if any)
- Your contact information

### Response Timeline

- **Acknowledgment:** Within 24 hours
- **Initial Assessment:** Within 72 hours
- **Fix Development:** 1-2 weeks (depending on severity)
- **Public Disclosure:** Coordinated with fix release

### Vulnerability Types

#### Critical (P0)
- Maintainer key compromise
- Signature threshold bypasses
- Governance rule tampering
- Configuration file injection
- Emergency mode abuse

#### High (P1)
- Maintainer key management issues
- Review period bypasses
- Economic node veto bypasses
- Configuration parsing vulnerabilities
- Access control issues

#### Medium (P2)
- Documentation errors
- Configuration inconsistencies
- Non-critical rule issues

### Security Considerations

#### Maintainer Keys
- Keys must be generated securely
- Keys must be stored securely (HSMs in production)
- Key rotation procedures must be followed
- Key compromise procedures must be documented

#### Signature Verification
- All signatures must be cryptographically verified
- Signature thresholds must be enforced
- No bypassing of signature requirements
- Audit trail must be maintained

#### Configuration Security
- Configuration files must be validated
- No injection vulnerabilities in parsers
- Secure configuration distribution
- Integrity checks on configuration

#### Governance Rules
- Rules must be tamper-evident
- No unauthorized rule changes
- Emergency procedures must be secure
- Economic node system must be protected

### Testing Requirements

Before reporting, please verify:
- [ ] The issue reproduces consistently
- [ ] The issue affects governance enforcement
- [ ] The issue is not already known
- [ ] The issue is not a feature request

### Security Updates

Security updates will be:
- Released as patch versions (0.1.x)
- Clearly marked as security fixes
- Backported to all supported versions
- Announced on our security mailing list

### Contact Information

- **Security Team:** security@btcdecoded.org
- **General Inquiries:** info@btcdecoded.org
- **Website:** https://btcdecoded.org

### Acknowledgments

We thank the security researchers who help keep Bitcoin governance secure through responsible disclosure.

---

**Remember:** This repository defines governance rules for the entire BTCDecoded ecosystem. Any vulnerabilities could compromise the entire governance system. Please report responsibly.

