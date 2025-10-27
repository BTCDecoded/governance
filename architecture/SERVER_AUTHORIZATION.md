# Server Authorization Architecture

## Overview

The server authorization system explicitly authorizes which servers can run critical Bitcoin jobs and operations. This provides an additional layer of security by ensuring only trusted, verified servers can perform governance operations.

## Purpose

Server authorization serves as a **security boundary mechanism** by:
- Explicitly authorizing which servers can run governance operations
- Preventing unauthorized servers from performing critical operations
- Providing audit trail of server operations
- Enabling rapid response to compromised servers

## Why Server Authorization?

### Security Benefits

1. **Attack Surface Reduction**: Only authorized servers can perform operations
2. **Compromise Detection**: Rapid detection of unauthorized server access
3. **Audit Trail**: Complete record of which server performed which operation
4. **Incident Response**: Quick isolation of compromised servers

### Operational Benefits

1. **Clear Ownership**: Each server has a known operator
2. **Contact Information**: Direct contact for operational issues
3. **Jurisdictional Clarity**: Legal jurisdiction for each server
4. **Maintenance Windows**: Coordinated maintenance schedules

## Server Registry

### Registry Structure

```json
{
  "version": "2024-01",
  "timestamp": "2024-01-15T10:30:00Z",
  "servers": [
    {
      "server_id": "governance-01",
      "operator": {
        "name": "Alice Smith",
        "jurisdiction": "United States",
        "contact": "alice@example.com",
        "organization": "BTCDecoded Foundation"
      },
      "keys": {
        "nostr_npub": "npub1abc123...",
        "ssh_fingerprint": "SHA256:xyz789..."
      },
      "infrastructure": {
        "vpn_ip": "10.0.0.2",
        "github_runner": true,
        "ots_enabled": true,
        "location": "US-East-1"
      },
      "status": "active",
      "added_at": "2024-01-01T00:00:00Z",
      "last_verified": "2024-01-15T10:30:00Z"
    }
  ],
  "approval_requirements": {
    "add_server": "4-of-5 maintainers",
    "remove_server": "3-of-5 maintainers",
    "compromise_server": "2-of-3 emergency keyholders"
  }
}
```

### Server Information

**Required Information:**
- **Server ID**: Unique identifier for the server
- **Operator Details**: Name, jurisdiction, contact information
- **Cryptographic Keys**: Nostr public key, SSH fingerprint
- **Infrastructure**: VPN IP, capabilities, location
- **Status**: Active, retiring, inactive, compromised

**Optional Information:**
- **Organization**: Company or organization name
- **Maintenance Window**: Preferred maintenance times
- **Backup Contacts**: Alternative contact information
- **Special Capabilities**: Unique server capabilities

## Authorization Process

### Adding Servers

1. **Application**: Operator submits server information
2. **Verification**: Maintainers verify operator identity
3. **Technical Review**: Verify server capabilities and security
4. **Approval**: Requires 4-of-5 maintainer signatures
5. **Onboarding**: Set up monitoring and access controls

### Removing Servers

1. **Initiation**: Maintainer or operator requests removal
2. **Graceful Shutdown**: 30-day notice for planned removal
3. **Data Migration**: Transfer data to other servers
4. **Approval**: Requires 3-of-5 maintainer signatures
5. **Decommissioning**: Remove from registry and monitoring

### Emergency Revocation

1. **Compromise Detection**: Identify compromised server
2. **Immediate Revocation**: 2-of-3 emergency keyholders
3. **Server Isolation**: Block all operations immediately
4. **Incident Response**: Investigate and contain breach
5. **Recovery**: Restore operations on clean servers

## Verification Process

### Server Verification

Before performing operations, servers must prove authorization:

1. **Registry Lookup**: Check server in authorized registry
2. **Key Verification**: Verify Nostr public key matches
3. **Status Check**: Ensure server status is "active"
4. **Signature Verification**: Verify operation signatures
5. **Timestamp Validation**: Check operation timestamps

### Operation Authorization

Each operation includes:
- **Server ID**: Identifies which server performed operation
- **Operation Type**: Type of operation performed
- **Timestamp**: When operation was performed
- **Signature**: Server's cryptographic signature
- **Authorization Proof**: Reference to server registry

## Integration with Governance

### Nostr Events

All server operations are published to Nostr with:
- **Server Authorization Tag**: Proof of server authorization
- **Operation Details**: What operation was performed
- **Timestamp**: When operation occurred
- **Signature**: Server's cryptographic signature

### Audit Logs

Server operations are logged with:
- **Server ID**: Which server performed operation
- **Operation Type**: Type of operation
- **Inputs/Outputs**: Operation inputs and outputs
- **Authorization Proof**: Reference to server registry
- **Timestamp**: When operation occurred

### Status Checks

GitHub status checks include:
- **Server Authorization**: Whether server is authorized
- **Server Status**: Current status of the server
- **Last Verification**: When server was last verified
- **Operator Contact**: Contact information for issues

## Security Considerations

### Key Management

- **Nostr Keys**: Used for signing operations and events
- **SSH Keys**: Used for server access and verification
- **Key Rotation**: Regular rotation of all keys
- **Key Storage**: Secure storage of private keys

### Access Control

- **VPN Access**: Servers must connect via VPN
- **IP Whitelisting**: Only authorized IPs can access
- **Multi-Factor Authentication**: MFA for all access
- **Audit Logging**: Log all access attempts

### Incident Response

- **Compromise Detection**: Automated detection of compromises
- **Immediate Revocation**: Quick revocation of compromised servers
- **Forensic Analysis**: Detailed analysis of security incidents
- **Recovery Procedures**: Clear procedures for recovery

## Monitoring and Compliance

### Server Monitoring

Monitor servers through:
- **Uptime Monitoring**: Server availability and performance
- **Operation Logging**: All operations performed by server
- **Security Scanning**: Regular security vulnerability scans
- **Compliance Checking**: Verify server meets requirements

### Compliance Enforcement

Enforce compliance through:
- **Automated Checks**: Regular automated compliance checks
- **Manual Audits**: Periodic manual security audits
- **Incident Response**: Rapid response to security incidents
- **Penalty System**: Consequences for non-compliance

## Operational Procedures

### Server Maintenance

- **Scheduled Maintenance**: Coordinate maintenance windows
- **Update Procedures**: Secure update procedures
- **Backup Procedures**: Regular backup of server data
- **Recovery Procedures**: Procedures for server recovery

### Emergency Procedures

- **Compromise Response**: Immediate response to compromises
- **Server Isolation**: Procedures for isolating compromised servers
- **Data Recovery**: Procedures for recovering from incidents
- **Communication**: Procedures for communicating incidents

## Future Enhancements

### Advanced Features

- **Automated Authorization**: Automatic authorization based on criteria
- **Dynamic Authorization**: Real-time authorization changes
- **Cross-Protocol**: Extend to other Bitcoin protocols
- **Federated Authorization**: Multi-organization authorization

### Integration Improvements

- **API Access**: Programmatic access to authorization data
- **Dashboard**: Web interface for authorization management
- **Mobile Apps**: Mobile interfaces for authorization
- **Analytics**: Comprehensive authorization analytics

## Examples

### Server Addition

```json
{
  "type": "server_add",
  "server": {
    "server_id": "governance-02",
    "operator": {
      "name": "Bob Johnson",
      "jurisdiction": "Switzerland",
      "contact": "bob@example.com"
    },
    "keys": {
      "nostr_npub": "npub1def456...",
      "ssh_fingerprint": "SHA256:abc123..."
    }
  },
  "approving_maintainers": ["maintainer_1", "maintainer_2", "maintainer_3", "maintainer_4"],
  "signatures": {
    "maintainer_1": "ed25519_signature_hex",
    "maintainer_2": "ed25519_signature_hex",
    "maintainer_3": "ed25519_signature_hex",
    "maintainer_4": "ed25519_signature_hex"
  },
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### Server Compromise

```json
{
  "type": "server_compromise",
  "server_id": "governance-01",
  "reason": "Suspected key compromise",
  "emergency_keyholders": ["emergency_1", "emergency_2"],
  "signatures": {
    "emergency_1": "ed25519_signature_hex",
    "emergency_2": "ed25519_signature_hex"
  },
  "timestamp": "2024-01-15T10:30:00Z"
}
```

## References

- [Server Authorization Configuration](../config/server-authorization.yml)
- [Emergency Procedures](../examples/emergency-response.md)
- [Maintainer Guide](../guides/MAINTAINER_GUIDE.md)
- [Security Guide](../../governance-app/SECURITY.md)
