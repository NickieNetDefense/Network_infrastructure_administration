# Firewall Policy Matrix

This document summarizes the primary inter-network firewall controls implemented in the Network Infrastructure Administration & Firewall Security lab.

The environment follows a **default-deny** security model. Traffic between network segments is permitted only where a documented business, infrastructure, or administrative requirement exists.

---

## Policy Summary

| Source Segment | Destination | Service / Port | Action | Purpose |
|---|---|---|---|---|
| Management | pfSense | HTTPS 443 | Allow | Restrict firewall administration to the dedicated Management network |
| Users | DC01 | DNS 53 TCP/UDP | Allow | Permit internal DNS resolution |
| Users | DC01 | Kerberos 88 TCP/UDP | Allow | Permit Active Directory authentication |
| Users | DC01 | LDAP 389 TCP/UDP | Allow | Permit domain controller discovery and directory services |
| Users | DC01 | Kerberos Password 464 TCP/UDP | Allow | Permit required Kerberos password operations |
| Users | Server Network | Unapproved services such as RDP 3389 | Deny | Prevent unnecessary lateral access to server systems |
| Security / Pentest | DC01 | Kerberos 88 | Allow | Permit controlled security assessment against an approved service |
| Security / Pentest | DC01 | Unapproved services | Deny | Restrict security testing to explicitly authorized services |
| Corporate Devices | Approved Internal Services | Explicitly permitted services | Allow | Support required corporate dependencies |
| Corporate Devices | Server Network | Unapproved services | Deny | Enforce least-privilege internal access |
| Guest | pfSense Guest Interface | DNS 53 TCP/UDP | Allow | Permit public DNS resolution through pfSense |
| Guest | RFC1918 Networks | Any | Deny | Prevent Guest access to internal private address space |
| Guest | Internet | Any | Allow | Provide Internet access while maintaining internal isolation |
| DMZ | Approved Internal Dependency | Explicitly permitted service | Allow | Support narrowly defined backend dependency |
| DMZ | Internal Networks | Other services | Deny | Limit exposure if a DMZ system is compromised |
| OpenVPN | Server Network | Authorized services | Allow | Permit authenticated remote access to protected resources |
| All Segments | Unmatched Traffic | Any | Default Deny | Require explicit authorization for inter-network communication |

---

# Reusable Firewall Objects

## RFC1918_NETWORKS

The `RFC1918_NETWORKS` alias contains the standard private IPv4 address ranges:

- `10.0.0.0/8`
- `172.16.0.0/12`
- `192.168.0.0/16`

This alias is used to prevent Guest clients from accessing internal private networks while still permitting outbound Internet access.

## AD_CORE_SERVICES

The `AD_CORE_SERVICES` alias groups required Active Directory services used by the User network to communicate with `DC01`.

Included services:

- Kerberos — `88`
- LDAP — `389`
- Kerberos password operations — `464`

Grouping related services into an alias simplifies firewall administration and reduces rule duplication.

---

# Security Design Principles

## Default Deny

Traffic not explicitly permitted by policy is denied by pfSense.

This reduces unintended connectivity between network zones and limits lateral movement.

## Least Privilege

Network access is granted only to the systems and services required for each segment.

Examples include:

- User systems can access required domain services without receiving unrestricted access to the Server network.
- Security/Pentest systems can assess approved services without broad access to all server ports.
- Guest clients can access the Internet while remaining isolated from private address space.
- DMZ systems receive only narrowly defined access to internal dependencies.

## Management Plane Isolation

pfSense administrative access is restricted to the Management network.

User-network attempts to reach the pfSense HTTPS management interface were denied.

## Segmentation

Separate network zones were created for:

- Management
- Servers
- Users
- Security / Pentest
- Corporate Devices
- Guest
- VoIP
- DMZ

Each zone was assigned an independent IPv4 subnet and pfSense gateway.

---

# Validation Methodology

Firewall policy was validated using both positive and negative tests.

Positive validation confirmed that approved traffic succeeded.

Negative validation confirmed that unapproved traffic was denied or filtered.

Tools used included:

- Windows PowerShell
- Kali Linux
- Nmap
- Wireshark
- pfSense firewall logs

Examples included:

- approved User-to-DC01 DNS
- approved Active Directory services
- blocked RDP access
- controlled Security/Pentest access
- Guest Internet access
- Guest internal-network denial
- DMZ restrictions
- VPN-to-server connectivity

---

# Representative Evidence

See the following screenshots in the repository:

- [67-pfsense-users-to-dc01-dns-rule.png](../screenshots/67-pfsense-users-to-dc01-dns-rule.png)
- [70-client01-pfsense-management-access-denied.png](../screenshots/70-client01-pfsense-management-access-denied.png)
- [71-pfsense-ad-domain-services-alias.png](../screenshots/71-pfsense-ad-domain-services-alias.png)
- [72-pfsense-users-to-dc01-domain-services-rule.png](../screenshots/72-pfsense-users-to-dc01-domain-services-rule.png)
- [75-pfsense-security-controlled-assessment-rule.png](../screenshots/75-pfsense-security-controlled-assessment-rule.png)
- [77-kali-unapproved-assessment-access-blocked.png](../screenshots/77-kali-unapproved-assessment-access-blocked.png)
- [81-client01-corporate-approved-and-denied-service-validation.png](../screenshots/81-client01-corporate-approved-and-denied-service-validation.png)
- [82-client01-dmz-restricted-internal-access-validation.png](../screenshots/82-client01-dmz-restricted-internal-access-validation.png)
- [83-pfsense-rfc1918-private-network-alias.png](../screenshots/83-pfsense-rfc1918-private-network-alias.png)
- [85-pfsense-guest-internet-and-internal-isolation-policy.png](../screenshots/85-pfsense-guest-internet-and-internal-isolation-policy.png)
- [86-client01-guest-internet-allowed-internal-denied.png](../screenshots/86-client01-guest-internet-allowed-internal-denied.png)
- [93-pfsense-firewall-log-default-deny-validation.png](../screenshots/93-pfsense-firewall-log-default-deny-validation.png)
- [95-openvpn-protected-resource-access-validation.png](../screenshots/95-openvpn-protected-resource-access-validation.png)

---

# Outcome

The resulting firewall policy demonstrates segmented network administration using explicit access control, least privilege, reusable aliases, management-plane isolation, default-deny enforcement, and operational validation.