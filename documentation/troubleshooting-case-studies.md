# Troubleshooting Case Studies

This document summarizes representative troubleshooting scenarios from the Network Infrastructure Administration & Firewall Security lab.

The goal is to demonstrate a structured administrative troubleshooting process rather than only successful configuration.

The general methodology used throughout the project was:

**Identify Symptoms → Verify Local Configuration → Test Network Path → Inspect Firewall Behavior → Isolate Root Cause → Apply Targeted Fix → Validate**

---

# Case Study 1 — Cross-VLAN DNS & Active Directory Discovery Failure

## Scenario

After moving `CLIENT01` to the User network, the workstation had valid IP addressing and could communicate with its local pfSense gateway.

However, domain-related services failed across the segmented network.

The environment included:

- `CLIENT01` — `10.10.30.10`
- User gateway — `10.10.30.1`
- `DC01` — `10.10.20.10`
- Internal domain — `ellistech.test`

---

## Symptoms

The client experienced:

- DNS requests to `10.10.20.10` timing out
- failure to resolve the internal domain
- Active Directory domain-controller discovery failure
- `nltest /dsgetdc:ellistech.test` returning an error

Because the workstation already had working local network connectivity, the issue was unlikely to be basic TCP/IP configuration.

---

## Investigation

Troubleshooting progressed through the network stack.

### 1. Verify Endpoint Configuration

The User endpoint was confirmed to have:

- the intended static IPv4 address
- correct `/24` subnet
- gateway `10.10.30.1`
- internal DNS target `10.10.20.10`

### 2. Verify Local Gateway Connectivity

Gateway reachability had already been validated.

This established that the endpoint could reach pfSense and that the User segment was operational.

### 3. Test Cross-VLAN DNS

DNS requests to `DC01` failed.

This isolated the issue to communication between the User and Server networks rather than the local endpoint segment.

### 4. Review Firewall Policy

The default-deny firewall policy did not yet permit DNS traffic between the User network and `DC01`.

A targeted firewall rule was added:

- Source: User network
- Destination: `10.10.20.10`
- Protocol: TCP/UDP
- Destination port: `53`

---

## First Validation

After the DNS rule was applied:

- internal DNS resolution succeeded
- `ellistech.test` resolved successfully
- TCP port 53 connectivity to `DC01` succeeded

However, domain-controller discovery continued to fail.

This demonstrated that working DNS alone was not sufficient for Active Directory functionality.

---

## Additional Investigation

Active Directory required additional services across the network boundary.

The required core services were grouped into the `AD_CORE_SERVICES` firewall alias.

The alias contained:

| Service | Port |
|---|---:|
| Kerberos | 88 |
| LDAP | 389 |
| Kerberos Password Operations | 464 |

A second firewall rule permitted the User network to reach these services on `DC01`.

---

## Final Validation

After the additional rule was applied:

- DNS resolution succeeded
- domain-controller discovery succeeded
- approved Active Directory services were reachable
- unrelated server services remained blocked

The solution restored required domain functionality without granting unrestricted User-to-Server access.

---

## Root Cause

The root cause was **incomplete inter-VLAN firewall policy**.

Basic IP routing was operational, but required application-layer dependencies had not yet been explicitly permitted through the default-deny firewall.

---

## Troubleshooting Path

**Endpoint Configuration → Gateway → Routing → DNS → Active Directory Dependencies → Firewall Policy → Validation**

---

## Evidence

Representative screenshots:

- [66-client01-cross-vlan-dns-ad-failure.png](../screenshots/66-client01-cross-vlan-dns-ad-failure.png)
- [67-pfsense-users-to-dc01-dns-rule.png](../screenshots/67-pfsense-users-to-dc01-dns-rule.png)
- [68-client01-cross-vlan-dns-validation-success.png](../screenshots/68-client01-cross-vlan-dns-validation-success.png)
- [69-client01-domain-controller-discovery-failure.png](../screenshots/69-client01-domain-controller-discovery-failure.png)
- [71-pfsense-ad-domain-services-alias.png](../screenshots/71-pfsense-ad-domain-services-alias.png)
- [72-pfsense-users-to-dc01-domain-services-rule.png](../screenshots/72-pfsense-users-to-dc01-domain-services-rule.png)
- [73-client01-domain-controller-discovery-success.png](../screenshots/73-client01-domain-controller-discovery-success.png)
- [74-client01-unapproved-server-port-blocked.png](../screenshots/74-client01-unapproved-server-port-blocked.png)

---

## Administrative Lesson

Successful infrastructure troubleshooting requires separating:

- basic network reachability
- DNS resolution
- application/service dependencies
- firewall policy

A broad allow rule would have restored connectivity faster, but it would have weakened segmentation.

The final remediation preserved least privilege by permitting only required services.

---

# Case Study 2 — Network Path & Firewall Availability

## Scenario

During User-network validation, `CLIENT01` had the expected network configuration but could not reach its default gateway.

Environment:

- `CLIENT01` — `10.10.30.10`
- User gateway — `10.10.30.1`
- Firewall — `FW01-pfSense`

---

## Symptoms

The client could not successfully ping:

`10.10.30.1`

The workstation appeared to have the correct IPv4 configuration, so the issue required investigation beyond static addressing.

---

## Investigation

### 1. Verify Local IP Configuration

The client configuration was reviewed and confirmed to match the User segment.

No addressing conflict or obvious subnet configuration problem was identified.

### 2. Check ARP Behavior

ARP was used to determine whether the endpoint could resolve the gateway's Layer 2 address.

Initially, the expected gateway relationship was unavailable.

This indicated that the problem could exist below the routing or firewall-policy layer.

### 3. Verify Infrastructure Availability

The pfSense virtual machine was found to be offline.

Because pfSense provides the Layer 3 gateway for the User network, the endpoint had no active gateway while the firewall was unavailable.

### 4. Restore pfSense

`FW01-pfSense` was started.

After the firewall returned online, the endpoint successfully learned the pfSense User-interface MAC address through ARP.

This confirmed that:

- the VirtualBox Internal Network was operating
- the endpoint NIC was attached correctly
- the pfSense interface was connected to the expected segment

---

## Secondary Issue

Although ARP now succeeded, ICMP gateway testing still failed.

This indicated that the infrastructure path had been restored, but traffic was being denied at a higher layer.

The pfSense default-deny policy was blocking the ICMP test.

A narrowly scoped rule was added:

- Interface: User network
- Source: User subnet
- Destination: User gateway address
- Protocol: ICMP

---

## Validation

After applying the ICMP rule:

- ARP resolution succeeded
- gateway ping succeeded
- endpoint-to-firewall connectivity was confirmed

---

## Root Cause

Two separate conditions affected the same symptom:

1. **pfSense was offline**, causing gateway unavailability.
2. After restoration, **firewall policy blocked ICMP**, causing the connectivity test to continue failing.

This demonstrated why troubleshooting should not stop after identifying the first problem.

---

## Troubleshooting Path

**Endpoint → Virtual NIC → Layer 2 Segment → Firewall Availability → ARP → Firewall Policy → Validation**

---

## Evidence

Representative screenshots:

- [58-client01-gateway-unreachable-pfsense-offline.png](../screenshots/58-client01-gateway-unreachable-pfsense-offline.png)
- [59-client01-user-segment-arp-validation.png](../screenshots/59-client01-user-segment-arp-validation.png)
- [60-pfsense-users-icmp-gateway-rule.png](../screenshots/60-pfsense-users-icmp-gateway-rule.png)
- [61-client01-user-segment-gateway-validation-success.png](../screenshots/61-client01-user-segment-gateway-validation-success.png)

---

## Administrative Lesson

Similar user symptoms can have causes at very different layers.

A failed gateway test might result from:

- incorrect IP configuration
- disconnected virtual NIC
- wrong network attachment
- Layer 2 failure
- unavailable firewall
- routing failure
- firewall policy

Using ARP before assuming a routing problem helped distinguish infrastructure availability from firewall enforcement.

---

# Additional Troubleshooting Evidence

The project contains several additional troubleshooting examples beyond the two primary case studies.

These include:

- initial internal connectivity failure during pfSense cutover
- Windows firewall ICMP investigation
- server-segment gateway validation
- Security/Pentest segment reachability
- DNS resolver troubleshooting for Guest Internet access
- incorrect Guest DNS client configuration
- OpenVPN certificate-authority mismatch during client export
- Wireshark capture-filter versus display-filter troubleshooting

The full evidence set is preserved in the `screenshots/` directory.

---

# Troubleshooting Principles Demonstrated

Across the project, troubleshooting consistently followed several principles:

## Verify Before Changing

Existing addressing, interface state, routes, and firewall behavior were checked before modifying configuration.

## Troubleshoot by Layer

Issues were separated into:

- endpoint configuration
- Layer 2 / ARP
- Layer 3 / routing
- DNS
- application/service requirements
- firewall policy
- infrastructure availability

## Prefer Narrow Remediation

Firewall issues were corrected with targeted rules rather than broad allow statements.

## Validate Both Positive and Negative Outcomes

A successful fix was not considered complete until:

- required traffic worked
- unauthorized traffic remained blocked

## Preserve Evidence

Failures, investigative steps, corrective actions, and successful validation were documented as part of the project evidence trail.

---

# Outcome

These scenarios demonstrate administrative troubleshooting across a segmented enterprise-style environment using:

- pfSense
- Windows PowerShell
- TCP/IP
- ARP
- DNS
- Active Directory service dependencies
- firewall policy
- VirtualBox networking
- structured validation

The emphasis throughout the project was not only restoring connectivity, but understanding **why** communication failed and correcting the specific layer responsible without weakening the overall security design.