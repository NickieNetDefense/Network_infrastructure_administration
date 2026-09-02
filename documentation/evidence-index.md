# Evidence Index

This document provides an index of the technical evidence captured during the Network Infrastructure Administration & Firewall Security project.

The complete screenshot archive is intentionally preserved as part of this repository.

The README highlights the strongest evidence for quick review, while this index provides a chronological record of the environment being built, segmented, secured, tested, troubleshot, and validated.

---

# Phase 1 — pfSense Deployment & Initial Network Cutover

| # | Screenshot | Evidence |
|---:|---|---|
| 01 | [01-pfsense-vm-confirmation.png](../screenshots/01-pfsense-vm-confirmation.png) | Initial pfSense virtual machine creation and resource configuration |
| 02 | [02-pfsense-installer-mounted.png](../screenshots/02-pfsense-installer-mounted.png) | pfSense installation media attached to the VM |
| 03 | [03-pfsense-network-adapters.png](../screenshots/03-pfsense-network-adapters.png) | Initial WAN and LAN virtual network-adapter configuration |
| 04 | [04-pfsense-installer-boot.png](../screenshots/04-pfsense-installer-boot.png) | pfSense installer successfully booted |
| 05 | [05-pfsense-lan-configured-10.10.10.1.png](../screenshots/05-pfsense-lan-configured-10.10.10.1.png) | LAN interface configured with `10.10.10.1` |
| 06 | [06-pfsense-final-console.png](../screenshots/06-pfsense-final-console.png) | Completed pfSense installation and console status |
| 07 | [07-pfsense-final-network-adapter1.png](../screenshots/07-pfsense-final-network-adapter1.png) | Final VirtualBox WAN adapter configuration |
| 08 | [08-pfsense-final-network-adapter2.png](../screenshots/08-pfsense-final-network-adapter2.png) | Final VirtualBox LAN adapter configuration |
| 09 | [09-DC01-pre-firewall-network-config.png](../screenshots/09-DC01-pre-firewall-network-config.png) | DC01 network configuration before pfSense cutover |
| 10 | [10-client01-pre-firewall-network-config.png](../screenshots/10-client01-pre-firewall-network-config.png) | CLIENT01 network configuration before pfSense cutover |
| 11 | [11-srv01-pre-firewall-network-config.png](../screenshots/11-srv01-pre-firewall-network-config.png) | SRV01 network configuration before pfSense cutover |
| 12 | [12-pfsense-lan-internal-network.png](../screenshots/12-pfsense-lan-internal-network.png) | pfSense LAN connected to the isolated ELLISTECH internal network |
| 13 | [13-dc01-srv01-client01-moved-to-ELLISTECH-LAN.png](../screenshots/13-dc01-srv01-client01-moved-to-ELLISTECH-LAN.png) | Existing systems migrated onto the pfSense-controlled internal network |
| 14 | [14-pfsense-post-cutover-console.png](../screenshots/14-pfsense-post-cutover-console.png) | pfSense operational after the internal-network cutover |
| 15 | [15-client02-internal-connectivity-failure.png](../screenshots/15-client02-internal-connectivity-failure.png) | Initial internal connectivity failure during cutover validation |

---

# Phase 2 — Initial Connectivity & Windows Firewall Troubleshooting

| # | Screenshot | Evidence |
|---:|---|---|
| 16 | [16-client01-dns-resolution-failure.png](../screenshots/16-client01-dns-resolution-failure.png) | DNS-resolution failure during early network troubleshooting |
| 17 | [17-dc01-internal-network-adapter-validation.png](../screenshots/17-dc01-internal-network-adapter-validation.png) | DC01 VirtualBox network attachment validation |
| 18 | [18-srv01-internal-network-adapter-validation.png](../screenshots/18-srv01-internal-network-adapter-validation.png) | SRV01 VirtualBox network attachment validation |
| 19 | [19-client01-internal-network-adapter-validation.png](../screenshots/19-client01-internal-network-adapter-validation.png) | CLIENT01 VirtualBox network attachment validation |
| 20 | [20-client01-arp-connectivity-investigation.png](../screenshots/20-client01-arp-connectivity-investigation.png) | ARP used to investigate Layer 2 connectivity |
| 21 | [21-dc01-to-client01-icmp-blocked.png](../screenshots/21-dc01-to-client01-icmp-blocked.png) | ICMP traffic blocked during endpoint connectivity testing |
| 22 | [22-dc01-to-client01-icmp-validation-success.png](../screenshots/22-dc01-to-client01-icmp-validation-success.png) | Successful connectivity after correcting ICMP policy |
| 23 | [23-srv01-connectivity-investigation.png](../screenshots/23-srv01-connectivity-investigation.png) | SRV01 connectivity investigation |
| 24 | [24-srv01-icmp-firewall-investigation.png](../screenshots/24-srv01-icmp-firewall-investigation.png) | Windows firewall identified as part of SRV01 ICMP troubleshooting |
| 25 | [25-srv01-icmp-firewall-rule-enabled.png](../screenshots/25-srv01-icmp-firewall-rule-enabled.png) | Required ICMP firewall rule enabled |
| 26 | [26-client01-to-srv01-icmp-validation-success.png](../screenshots/26-client01-to-srv01-icmp-validation-success.png) | Successful CLIENT01-to-SRV01 connectivity after remediation |

---

# Phase 3 — Enterprise VLAN Architecture & Core pfSense Services

| # | Screenshot | Evidence |
|---:|---|---|
| 27 | [27-kali-security-vm-final-configuration.png](../screenshots/27-kali-security-vm-final-configuration.png) | Kali Linux security-assessment VM configuration |
| 28 | [28-pfsense-management-dashboard.png](../screenshots/28-pfsense-management-dashboard.png) | pfSense WebGUI administration and system status |
| 29 | [29-pfsense-vlan20-servers-created.png](../screenshots/29-pfsense-vlan20-servers-created.png) | Server VLAN creation |
| 30 | [30-pfsense-enterprise-vlan-table.png](../screenshots/30-pfsense-enterprise-vlan-table.png) | Enterprise VLAN architecture covering Management, Servers, Users, Security, Corporate, Guest, VoIP, and DMZ |
| 31 | [31-pfsense-servers-interface-configured.png](../screenshots/31-pfsense-servers-interface-configured.png) | Server-segment pfSense interface configuration |
| 32 | [32-pfsense-vlan-interface-assignments.png](../screenshots/32-pfsense-vlan-interface-assignments.png) | VLAN interfaces assigned in pfSense |
| 33 | [33-pfsense-kea-dhcp-backend-switch-recommended.png](../screenshots/33-pfsense-kea-dhcp-backend-switch-recommended.png) | Identification of deprecated ISC DHCP backend and recommended Kea migration |
| 34 | [34-pfsense-kea-dhcp-backend-enabled.png](../screenshots/34-pfsense-kea-dhcp-backend-enabled.png) | Kea DHCP backend enabled |
| 35 | [35-pfsense-users-dhcp-configuration.png](../screenshots/35-pfsense-users-dhcp-configuration.png) | DHCP scope configuration for the User network |
| 36 | [36-pfsense-vland-routing-table.png](../screenshots/36-pfsense-vland-routing-table.png) | pfSense routing table demonstrating Layer 3 network paths |
| 37 | [37-pfsense-vlan-interface-status.png](../screenshots/37-pfsense-vlan-interface-status.png) | VLAN and interface operational status |

---

# Phase 4 — Dedicated Management Network

| # | Screenshot | Evidence |
|---:|---|---|
| 38 | [38-mgmt01-virtualbox-configuration.png](../screenshots/38-mgmt01-virtualbox-configuration.png) | Dedicated MGMT01 workstation VM configuration |
| 39 | [39-mgmt01-management-network-adapter.png](../screenshots/39-mgmt01-management-network-adapter.png) | MGMT01 attached to the Management network |
| 40 | [40-mgmt01-static-management-address.png](../screenshots/40-mgmt01-static-management-address.png) | Static Management address `10.10.10.10/24` |
| 41 | [41-mgmt01-pfsense-administration-validation.png](../screenshots/41-mgmt01-pfsense-administration-validation.png) | Successful pfSense administration from the dedicated Management workstation |

---

# Phase 5 — Live Segment Implementation

| # | Screenshot | Evidence |
|---:|---|---|
| 42 | [42-pfsense-server-segment-adapter.png](../screenshots/42-pfsense-server-segment-adapter.png) | Dedicated Server-segment virtual interface |
| 43 | [43-pfsense-user-segment-adapter.png](../screenshots/43-pfsense-user-segment-adapter.png) | Dedicated User-segment virtual interface |
| 44 | [44-pfsense-security-segment-adapter-cli.png](../screenshots/44-pfsense-security-segment-adapter-cli.png) | Security-segment interface validated from pfSense CLI |
| 45 | [45-pfsense-physical-interface-mac-mapping.png](../screenshots/45-pfsense-physical-interface-mac-mapping.png) | VirtualBox-to-pfSense interface mapping using MAC addresses |
| 46 | [46-pfsense-live-segment-nic-mapping.png](../screenshots/46-pfsense-live-segment-nic-mapping.png) | Physical virtual NIC mapping for live network segments |
| 47 | [47-pfsense-live-segment-interface-assignments.png](../screenshots/47-pfsense-live-segment-interface-assignments.png) | Live segments assigned to pfSense interfaces |
| 48 | [48-pfsense-live-segment-ip-validation.png](../screenshots/48-pfsense-live-segment-ip-validation.png) | Gateway addressing validated across live segments |

---

# Phase 6 — Server Segment Migration & Validation

| # | Screenshot | Evidence |
|---:|---|---|
| 49 | [49-dc01-server-segment-network-configuration.png](../screenshots/49-dc01-server-segment-network-configuration.png) | DC01 migrated to `10.10.20.10/24` on the Server network |
| 50 | [50-dc01-server-segment-arp-validation.png](../screenshots/50-dc01-server-segment-arp-validation.png) | DC01 successfully learned the Server gateway through ARP |
| 51 | [51-pfsense-servers-icmp-gateway-rule.png](../screenshots/51-pfsense-servers-icmp-gateway-rule.png) | Narrow Server-to-gateway ICMP validation rule |
| 52 | [52-dc01-server-segment-gateway-validation-success.png](../screenshots/52-dc01-server-segment-gateway-validation-success.png) | Successful DC01 Server-gateway connectivity |
| 53 | [53-dc01-old-management-nic-disabled.png](../screenshots/53-dc01-old-management-nic-disabled.png) | Legacy flat-network NIC disabled on DC01 |
| 54 | [54-dc01-server-segment-final-network-state.png](../screenshots/54-dc01-server-segment-final-network-state.png) | Final DC01 network state after segmentation |
| 55 | [55-srv01-old-management-nic-disabled.png](../screenshots/55-srv01-old-management-nic-disabled.png) | Legacy flat-network NIC disabled on SRV01 |
| 56 | [56-srv01-server-segment-connectivity-validation.png](../screenshots/56-srv01-server-segment-connectivity-validation.png) | SRV01 Server-network connectivity validation |

---

# Phase 7 — User Segment & Network-Path Troubleshooting

| # | Screenshot | Evidence |
|---:|---|---|
| 57 | [57-client01-user-segment-network-configuration.png](../screenshots/57-client01-user-segment-network-configuration.png) | CLIENT01 moved to `10.10.30.10/24` on the User network |
| 58 | [58-client01-gateway-unreachable-pfsense-offline.png](../screenshots/58-client01-gateway-unreachable-pfsense-offline.png) | Gateway failure caused by unavailable pfSense infrastructure |
| 59 | [59-client01-user-segment-arp-validation.png](../screenshots/59-client01-user-segment-arp-validation.png) | ARP validation after restoring pfSense |
| 60 | [60-pfsense-users-icmp-gateway-rule.png](../screenshots/60-pfsense-users-icmp-gateway-rule.png) | User-network ICMP gateway rule |
| 61 | [61-client01-user-segment-gateway-validation-success.png](../screenshots/61-client01-user-segment-gateway-validation-success.png) | Successful User-network gateway validation |

---

# Phase 8 — Security / Pentest Segment

| # | Screenshot | Evidence |
|---:|---|---|
| 62 | [62-kali-security-segment-network-configuration.png](../screenshots/62-kali-security-segment-network-configuration.png) | Kali configured as `10.10.40.10/24` |
| 63 | [63-kali-security-segment-neighbor-validation.png](../screenshots/63-kali-security-segment-neighbor-validation.png) | Kali neighbor/ARP validation against the Security gateway |
| 64 | [64-pfsense-security-icmp-gateway-rule.png](../screenshots/64-pfsense-security-icmp-gateway-rule.png) | Security-network ICMP gateway-validation rule |
| 65 | [65-kali-security-segment-gateway-validation-success.png](../screenshots/65-kali-security-segment-gateway-validation-success.png) | Successful Kali-to-Security-gateway connectivity |

---

# Phase 9 — Cross-VLAN DNS & Active Directory Policy

| # | Screenshot | Evidence |
|---:|---|---|
| 66 | [66-client01-cross-vlan-dns-ad-failure.png](../screenshots/66-client01-cross-vlan-dns-ad-failure.png) | Initial cross-VLAN DNS and AD service failure |
| 67 | [67-pfsense-users-to-dc01-dns-rule.png](../screenshots/67-pfsense-users-to-dc01-dns-rule.png) | Least-privilege User-to-DC01 DNS rule |
| 68 | [68-client01-cross-vlan-dns-validation-success.png](../screenshots/68-client01-cross-vlan-dns-validation-success.png) | Successful cross-VLAN DNS resolution after remediation |
| 69 | [69-client01-domain-controller-discovery-failure.png](../screenshots/69-client01-domain-controller-discovery-failure.png) | Domain-controller discovery still failing after DNS remediation |
| 70 | [70-client01-pfsense-management-access-denied.png](../screenshots/70-client01-pfsense-management-access-denied.png) | User network denied access to pfSense management interface |
| 71 | [71-pfsense-ad-domain-services-alias.png](../screenshots/71-pfsense-ad-domain-services-alias.png) | `AD_CORE_SERVICES` firewall alias |
| 72 | [72-pfsense-users-to-dc01-domain-services-rule.png](../screenshots/72-pfsense-users-to-dc01-domain-services-rule.png) | User-to-DC01 Active Directory service rule |
| 73 | [73-client01-domain-controller-discovery-success.png](../screenshots/73-client01-domain-controller-discovery-success.png) | Successful AD domain-controller discovery |
| 74 | [74-client01-unapproved-server-port-blocked.png](../screenshots/74-client01-unapproved-server-port-blocked.png) | Unapproved User-to-Server service remains blocked |

---

# Phase 10 — Controlled Security Assessment

| # | Screenshot | Evidence |
|---:|---|---|
| 75 | [75-pfsense-security-controlled-assessment-rule.png](../screenshots/75-pfsense-security-controlled-assessment-rule.png) | Explicit Security/Pentest assessment rule |
| 76 | [76-kali-approved-assessment-access-success.png](../screenshots/76-kali-approved-assessment-access-success.png) | Kali successfully reaches an approved server service |
| 77 | [77-kali-unapproved-assessment-access-blocked.png](../screenshots/77-kali-unapproved-assessment-access-blocked.png) | Kali denied access to an unapproved server service |

---

# Phase 11 — Corporate, Guest & DMZ Implementation

| # | Screenshot | Evidence |
|---:|---|---|
| 78 | [78-pfsense-corporate-segment-nic-mapping.png](../screenshots/78-pfsense-corporate-segment-nic-mapping.png) | Corporate network mapped to dedicated pfSense interface |
| 79 | [79-pfsense-guest-dmz-segment-nics-created.png](../screenshots/79-pfsense-guest-dmz-segment-nics-created.png) | Guest and DMZ VirtualBox network interfaces created |
| 80 | [80-client01-corporate-segment-network-validation.png](../screenshots/80-client01-corporate-segment-network-validation.png) | Representative Corporate endpoint network validation |
| 81 | [81-client01-corporate-approved-and-denied-service-validation.png](../screenshots/81-client01-corporate-approved-and-denied-service-validation.png) | Corporate endpoint allowed approved service while unapproved service remained blocked |
| 82 | [82-client01-dmz-restricted-internal-access-validation.png](../screenshots/82-client01-dmz-restricted-internal-access-validation.png) | DMZ endpoint permitted narrowly defined access while broader internal access remained restricted |
| 83 | [83-pfsense-rfc1918-private-network-alias.png](../screenshots/83-pfsense-rfc1918-private-network-alias.png) | Reusable RFC1918 private-network firewall alias |
| 84 | [84-pfsense-rfc1918-alias-private-network-IPtypes.png](../screenshots/84-pfsense-rfc1918-alias-private-network-IPtypes.png) | RFC1918 address classes and private ranges documented in pfSense |
| 85 | [85-pfsense-guest-internet-and-internal-isolation-policy.png](../screenshots/85-pfsense-guest-internet-and-internal-isolation-policy.png) | Guest DNS exception, RFC1918 block, and Internet allow policy |
| 86 | [86-client01-guest-internet-allowed-internal-denied.png](../screenshots/86-client01-guest-internet-allowed-internal-denied.png) | Guest endpoint successfully reaches Internet while internal networks remain inaccessible |

---

# Phase 12 — DNS, NAT & Internet Connectivity

| # | Screenshot | Evidence |
|---:|---|---|
| 87 | [87-pfsense-public-dns-resolution-validation.png](../screenshots/87-pfsense-public-dns-resolution-validation.png) | pfSense successfully resolves public DNS |
| 88 | [88-pfsense-automatic-outbound-nat-configuration.png](../screenshots/88-pfsense-automatic-outbound-nat-configuration.png) | Automatic Outbound NAT enabled |
| 89 | [89-pfsense-automatic-outbound-rules.png](../screenshots/89-pfsense-automatic-outbound-rules.png) | Automatically generated NAT rules for internal networks |
| 90 | [90-client01-guest-dns-and-internet-validation.png](../screenshots/90-client01-guest-dns-and-internet-validation.png) | Guest endpoint successfully resolves DNS and reaches public Internet destinations |

---

# Phase 13 — Nmap Security Validation

| # | Screenshot | Evidence |
|---:|---|---|
| 91 | [91-kali-nmap-firewall-policy-validation.png](../screenshots/91-kali-nmap-firewall-policy-validation.png) | Nmap validates allowed Kerberos exposure while unapproved DNS, LDAP, SMB, and RDP services remain filtered |

Nmap test:

    nmap -Pn -sT -p 53,88,389,445,3389 10.10.20.10

Observed:

- `88/tcp` — Open
- `53/tcp` — Filtered
- `389/tcp` — Filtered
- `445/tcp` — Filtered
- `3389/tcp` — Filtered

This provides independent validation of the Security/Pentest firewall policy.

---

# Phase 14 — Wireshark Packet Analysis

| # | Screenshot | Evidence |
|---:|---|---|
| 92 | [92-wireshark-approved-kerberos-traffic-analysis.png](../screenshots/92-wireshark-approved-kerberos-traffic-analysis.png) | Packet-level validation of approved TCP/88 communication between Security and Server networks |

Observed TCP exchange:

    10.10.40.10 → 10.10.20.10   SYN
    10.10.20.10 → 10.10.40.10   SYN, ACK
    10.10.40.10 → 10.10.20.10   ACK

This confirms successful establishment of the approved Kerberos connection through pfSense.

---

# Phase 15 — Firewall Logging

| # | Screenshot | Evidence |
|---:|---|---|
| 93 | [93-pfsense-firewall-log-default-deny-validation.png](../screenshots/93-pfsense-firewall-log-default-deny-validation.png) | pfSense records blocked DMZ-originated traffic matching the default-deny firewall rule |

The log provides operational evidence of:

- Interface
- Source
- Destination
- Destination port
- Matched firewall rule
- Deny action

This demonstrates that denied traffic was not only blocked by policy, but also recorded for administrative review and troubleshooting.

---
# Phase 16 — Secure Remote Access

| # | Screenshot | Evidence |
|---:|---|---|
| 94 | [94-openvpn-client-connected-tunnel-ip.png](../screenshots/94-openvpn-client-connected-tunnel-ip.png) | Windows OpenVPN client connected and assigned tunnel address `10.99.20.2` |
| 95 | [95-openvpn-protected-resource-access-validation.png](../screenshots/95-openvpn-protected-resource-access-validation.png) | VPN client successfully reaches an approved protected service on `DC01` through the OpenVPN tunnel |

The validation confirms the secure remote-access path:

**Remote Client → OpenVPN Tunnel → pfSense → Protected Server Resource**

This demonstrates successful tunnel establishment, VPN addressing, and authorized access to an internal resource.

---
# Competency Evidence Map

The screenshots collectively provide evidence across the following technical competencies:

| Competency | Representative Evidence |
|---|---|
| Network Architecture | 30, 32, 36 |
| VLANs & Segmentation | 29–32, 42–48 |
| TCP/IP & Subnetting | 30, 40, 49, 57, 62 |
| Routing | 36, 50–52, 59–61 |
| ARP | 20, 50, 59, 63 |
| DHCP | 33–35 |
| DNS | 16, 66–68, 87, 90 |
| Active Directory Network Dependencies | 66–74 |
| pfSense Administration | 28, 31–37, 41 |
| Firewall Policy | 51, 60, 64, 67, 72, 75, 85 |
| Least Privilege | 74, 77, 81, 82, 86 |
| Management Isolation | 41, 70 |
| Guest Isolation | 83–86, 90 |
| DMZ Security | 79, 82, 93 |
| NAT | 88–90 |
| Kali Linux | 27, 62–65, 76–77, 91–92 |
| Nmap | 91 |
| Wireshark | 92 |
| Firewall Logging | 93 |
| OpenVPN | 94–95 |
| Administrative Troubleshooting | 15–26, 58–61, 66–74 |

---
# Evidence Philosophy

Not every screenshot in this repository is intended for display in the primary README.

The evidence archive serves three purposes:

1. **Portfolio Evidence**  
   Demonstrates hands-on implementation rather than certification knowledge alone.

2. **Technical History**  
   Preserves configuration decisions, failures, troubleshooting paths, corrective actions, and successful validation.

3. **Living Lab Documentation**  
   Provides a baseline that can be expanded as the environment evolves with additional networking technologies, firewall vendors, monitoring systems, and security controls.

The README presents a curated technical story for quick review, while this evidence index preserves the complete project lifecycle.

---
# Project Validation Summary

The evidence demonstrates an end-to-end network administration workflow:

**Design → Deploy → Segment → Address → Route → Secure → Connect → Test → Analyze → Log → Troubleshoot → Validate**

The final environment demonstrates practical administration using:

- pfSense
- VLAN architecture
- TCP/IP
- IPv4 subnetting
- Routing
- DHCP
- DNS
- NAT
- Firewall policy
- OpenVPN
- Kali Linux
- Nmap
- Wireshark
- Oracle VirtualBox
- Windows infrastructure

---
# Final Outcome

This evidence set demonstrates practical network administration across a segmented enterprise-style environment.

The project shows the ability to:

- Build and administer segmented network infrastructure
- Configure routing and gateway services
- Implement DHCP and DNS dependencies
- Enforce least-privilege firewall policy
- Configure NAT and Internet access
- Deploy secure remote-access VPN
- Validate network exposure with Nmap
- Analyze network traffic with Wireshark
- Inspect and correlate firewall logs
- Troubleshoot connectivity problems by network layer
- Validate both successful and denied traffic paths

The complete evidence archive is preserved so the repository can continue to grow as additional networking technologies, firewall platforms, monitoring systems, and administrative scenarios are added.

The complete evidence archive is preserved so the repository can continue to grow as additional networking technologies and administrative scenarios are added.