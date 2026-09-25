<div align="center">

# ⚙️ Enterprise Network Services, Telemetry & Wireless Labs

[![Infrastructure](https://img.shields.io/badge/Infrastructure-Network_Services_&_Telemetry-00599C?style=for-the-badge&logo=cisco&logoColor=white)](https://github.com/abdulwahabsaim)
[![Certification](https://img.shields.io/badge/Certification-Cisco_CCNA_200--301-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)](https://cisco.com)
[![Verified Labs](https://img.shields.io/badge/Verified_Labs-5_Production_Scenarios-brightgreen?style=for-the-badge)]()
[![Location](https://img.shields.io/badge/Location-Netherlands_🇳🇱-orange?style=for-the-badge)]()
[![Author](https://img.shields.io/badge/Author-Abdul_Wahab_Saim-blueviolet?style=for-the-badge)](https://linkedin.com/in/abdulwahabsaim)

<p align="center">
  <b>A comprehensive, production-grade repository of 5 hands-on enterprise network services, centralized IPAM, cryptographic time synchronization, SIEM event telemetry, and controller-based wireless labs designed for Level 1 / Level 2 Network Operations Center (NOC) and Infrastructure roles.</b>
</p>

[Core Domains](#-core-technical-domains) • [Skills Matrix](#-topics--skills-coverage-matrix) • [Detailed Lab Directory](#-detailed-laboratory-catalog-5-scenarios) • [Services Architecture Matrix](#-core-network-services--protocols-matrix) • [NOC Runbook](#-enterprise-services--telemetry-cli-runbook)

</div>

---

## 📌 Executive Summary

Routing fabrics and switching boundaries are powerless without the fundamental application and telemetry services that support end-user compute and infrastructure health. In production enterprise environments, network reliability depends on automated IP address management (IPAM), sub-millisecond cryptographic time synchronization, centralized SIEM event ingestion, deterministic name resolution, and controller-based wireless management.

This repository documents a systematic collection of **5 production-style core service and telemetry labs** designed and verified in Cisco Packet Tracer and GNS3.

Every lab adheres to enterprise operational standards:
* **Centralized Management:** Consolidating DHCP scopes, authoritative DNS records, and WLC policies within data center boundaries.
* **Cross-WAN Service Delivery:** Utilizing UDP helper gateways (`ip helper-address`) to forward client broadcast transactions across routed transit hops.
* **Telemetry & Security Auditing:** Hardening chronometry via MD5-authenticated NTP hierarchies (Stratum 1–3) and streaming millisecond-accurate RFC 5424 Syslog traps to remote collectors (UDP 514).
* **Controller-Based Wireless:** Decoupling RF real-time MAC functions from control logic using Split-MAC CAPWAP tunnels and dynamic 802.1Q VLAN mappings.

---

## 🧱 Core Technical Domains

```text
                               ┌──────────────────────────────────────────────────────────┐
                               │       ENTERPRISE NETWORK SERVICES & TELEMETRY            │
                               └────────────────────────────┬─────────────────────────────┘
                                                            │
         ┌──────────────────────────┬───────────────────────┴───────────────┬──────────────────────────┐
         │                          │                                       │                          │
         ▼                          ▼                                       ▼                          ▼
┌────────────────────┐      ┌────────────────────┐                 ┌────────────────────┐      ┌────────────────────┐
│ CLIENT LIFECYCLE   │      │ TIME & TELEMETRY   │                 │ NAME RESOLUTION &  │      │ CENTRALIZED WLAN   │
│ & CENTRAL IPAM     │      │ AUDITING (NTP/LOG) │                 │ WEB HOSTING        │      │ (WLC & CAPWAP)     │
├────────────────────┤      ├────────────────────┤                 ├────────────────────┤      ├────────────────────┤
│• DHCP DORA Process │      │• NTP Stratum 1-3   │                 │• Authoritative DNS │      │• Cisco 3504 WLC    │
│• Multi-Scope Pools │      │• MD5 Key Auth      │                 │• Forward A-Records │      │• Lightweight APs   │
│• IP Helper-Address │      │• Hardware RTC Sync │                 │• HTTP/HTTPS Hosting│      │• Split-MAC CAPWAP  │
│• Excluded Ranges   │      │• Syslog Levels 0-7 │                 │• FQDN Verification │      │• Native VLAN Trunk │
│• Router DHCP Client│      │• Remote Traps (514)│                 │• End-to-End Testing│      │• Dynamic VLAN SSIDs│
└────────────────────┘      └────────────────────┘                 └────────────────────┘      └────────────────────┘
```

---

## 🎯 Topics & Skills Coverage Matrix

Use this matrix to locate specific service protocols, telemetry mechanisms, and operational scenarios across the 5 laboratories:

| Technical Service / Feature | Primary Protocol / Port | Implemented In | Key Cisco IOS / Appliance Commands |
| :--- | :--- | :--- | :--- |
| **Integrated Client Stack Lifecycle** | DHCP (67/68), DNS (53), HTTP (80) | [Lab 01](./01-core-network-services-dhcp-dns-http/) | `ip dhcp pool`, `dns-server`, `default-router` |
| **Cross-WAN DHCP Relay Agent** | DHCP / BOOTP (UDP 67/68) | [Lab 02](./02-centralized-dhcp-relay-ip-helper/) | `ip helper-address [server-ip]`, `ip address dhcp` |
| **Cryptographic Time Distribution** | NTPv4 (UDP 123) | [Lab 03](./03-ntp-stratum-hierarchy-authentication/) | `ntp authenticate`, `ntp trusted-key`, `ntp master`, `update-calendar` |
| **Enterprise SIEM Event Logging** | Syslog (UDP 514) | [Lab 04](./04-centralized-syslog-telemetry/) | `service timestamps log datetime msec`, `logging [host]`, `logging trap` |
| **Controller-Based Wireless (WLAN)**| CAPWAP (UDP 5246/5247) | [Lab 05](./05-enterprise-wlc-centralized-wireless/) | `switchport trunk native vlan`, WLC Dynamic Interfaces, WPA2-PSK |

---

## 🗺️ Detailed Laboratory Catalog (5 Scenarios)

### 🔹 [01-core-network-services-dhcp-dns-http](./01-core-network-services-dhcp-dns-http/)
* **Focus:** End-to-End Client Lifecycle & Core Application Stack Integration
* **Hardware:** Catalyst 2960 Switch, 3x Dedicated Enterprise Servers (DHCP, DNS, Web), Client Workstations
* **Key Topics Covered:** The complete 4-step DHCP D.O.R.A handshake (Discover, Offer, Request, Acknowledge), DNS forward resolution (A-Records mapped to FQDNs), HTTP/HTTPS web application hosting, default gateway propagation, and verifying complete client access lifecycle from physical link-up to browser rendering.

### 🔹 [02-centralized-dhcp-relay-ip-helper](./02-centralized-dhcp-relay-ip-helper/)
* **Focus:** Centralized Data Center IPAM & Cross-WAN DHCP Relay Forwarding
* **Hardware:** 2x Cisco 2911 Routers (R1 Branch Relay & R2 Central Server), 2x Catalyst 2960 Switches
* **Key Topics Covered:** Centralizing dynamic address pools within data center infrastructure, configuring multiple IP scopes and reservation exclusions, enabling `ip helper-address` on branch gateways to convert Layer 2 local broadcasts into routable unicast UDP packets across WAN boundaries, and configuring edge router interfaces to lease dynamic WAN addresses (`ip address dhcp`).

### 🔹 [03-ntp-stratum-hierarchy-authentication](./03-ntp-stratum-hierarchy-authentication/)
* **Focus:** NTP Stratum Hierarchy (1–3), MD5 Cryptographic Authentication & RTC Sync
* **Hardware:** 2x Cisco 2911 Routers, External Stratum 1 Reference Clock
* **Key Topics Covered:** Hierarchical time distribution mechanics (Stratum 1 Reference ➔ Stratum 2 Border Master ➔ Stratum 3 Internal Client), enforcing MD5 cryptographic authentication (`ntp authentication-key`, `ntp authenticate`, `ntp trusted-key`) to prevent time-shifting attacks, updating hardware real-time clock calendars (`ntp update-calendar`), and evaluating association metrics (octal `reach 377`, dispersion, offset).

### 🔹 [04-centralized-syslog-telemetry](./04-centralized-syslog-telemetry/)
* **Focus:** Centralized Event Logging, Millisecond Timestamps & RFC 5424 Severity Levels
* **Hardware:** Cisco 2911 Router, Dedicated Syslog Server Daemon
* **Key Topics Covered:** Enforcing millisecond precision chronological timestamps (`service timestamps log datetime msec`), configuring local circular RAM buffers (`logging buffered 4096`), offloading facility traps across UDP port 514 to a centralized collector (`logging trap debugging`), dissecting the standardized message format (Timestamp, Facility, Severity 0–7, Mnemonic, Body), and utilizing `terminal monitor` for real-time remote VTY triage.

### 🔹 [05-enterprise-wlc-centralized-wireless](./05-enterprise-wlc-centralized-wireless/)
* **Focus:** Centralized Enterprise Wireless, Split-MAC CAPWAP & Cisco 3504 WLC
* **Hardware:** Cisco 3504 WLC, Catalyst 3650 Multilayer Switch, 2x Lightweight APs (LAPs), Wireless Clients
* **Key Topics Covered:** The Split-MAC architecture (LAPs handling real-time 802.11 framing, WLC handling centralized management/authentication), establishing CAPWAP tunnels (UDP 5246 Control / UDP 5247 Data), configuring 802.1Q trunking with **Native VLAN 10** for untagged WLC management, mapping logical dynamic interfaces to discrete VLANs (VLAN 100 Internal, VLAN 200 Guest), and deploying dual SSIDs secured by WPA2-Personal (AES).

---

## 📊 Core Network Services & Protocols Matrix

A quick-reference architectural comparison of the core enterprise services and telemetry protocols implemented across this repository:

| Service / Protocol | Default Transport & Port | Primary Architectural Role | Security / Operational Best Practice | Standard / RFC |
| :--- | :--- | :--- | :--- | :--- |
| **DHCP** | **UDP 67 (Server) / 68 (Client)** | Dynamic IP, Mask, Gateway & DNS configuration | Exclude static management ranges; enforce DHCP Snooping | RFC 2131 |
| **DHCP Relay** | **UDP 67 (Unicast)** | Relays client broadcasts across Layer 3 boundaries | Restrict forwarded UDP protocols with `no ip forward-protocol` | RFC 1542 |
| **DNS** | **UDP / TCP 53** | Hostname to IP address forward/reverse resolution | Maintain redundant forwarders (e.g., Primary + Secondary) | RFC 1035 |
| **NTP** | **UDP 123** | Enterprise-wide clock synchronization | Enforce MD5 cryptographic keys; sync to battery RTC | RFC 5905 |
| **Syslog** | **UDP 514** | Centralized event logging and security auditing | Configure millisecond timestamps; retain logs off-device | RFC 5424 |
| **CAPWAP Control** | **UDP 5246 (DTLS Encrypted)** | WLC-to-AP management, channel/power orchestration | Keep management untagged on Native VLAN; ensure MTU $\ge 1500$ | RFC 5415 |
| **CAPWAP Data** | **UDP 5247 (Encapsulated)** | Tunnels client data frames from AP back to WLC | Map discrete SSIDs directly to segmented corporate VLANs | RFC 5416 |

---

## 🧰 Enterprise Services & Telemetry CLI Runbook

Essential Cisco IOS diagnostic commands demonstrated and documented across these 5 laboratories:

```text
================================================================================
CATEGORY 1: IPAM, DHCP & CLIENT BINDINGS
================================================================================
show ip dhcp binding                  # Displays all active MAC-to-IP leases allocated by the server
show ip dhcp pool                     # Displays subnet utilization, leased addresses, and excluded ranges
show ip dhcp server statistics        # Displays total DHCP DISCOVER, OFFER, REQUEST, and ACK packet counters
show ip interface [id]                # Confirms if an "ip helper-address" is actively bound to the gateway

================================================================================
CATEGORY 2: TIME SYNCHRONIZATION & TELEMETRY
================================================================================
show ntp status                       # Validates clock sync state, local Stratum level, offset, and ref clock
show ntp associations                 # Displays peer table, configured status (~), active peer (*), and reach (377)
show ntp associations detail          # Displays packet counters, authentication status, and filter dispersion
show clock detail                     # Displays current system time and validates source (NTP vs hardware RTC)
show logging                          # Displays logging status, drop counters, trap level, and dumps the RAM buffer
terminal monitor                      # Enables real-time Syslog printing to the current VTY/SSH session

================================================================================
CATEGORY 3: ENTERPRISE WIRELESS & UNDERLAY INFRASTRUCTURE
================================================================================
show interfaces trunk                 # Verifies 802.1Q trunking to WLC and confirms Native VLAN matches Management
show interfaces [id] switchport       # Validates access vs trunk mode, Native VLAN, and DTP state on AP ports
show vlan brief                       # Confirms corporate, guest, and management wireless VLANs exist in database
show ip interface brief               # Validates SVI default gateway status for all routed wireless subnets
```

---

## 📁 Standardized 4-File Package Structure

To maintain production standards, every lab subfolder in this repository is strictly organized as a self-contained 4-file unit:

```text
0X-lab-topic-name/
├── README.md                      # In-depth technical documentation, schema tables & CLI proof
├── topology.png                   # Clean, 16:9 cropped enterprise topology diagram
├── <lab-name>.pkt                 # Completed, verified Cisco Packet Tracer simulation file
└── <device>-config.ios            # Syntax-highlighted, clean running configurations (paste-ready)
```

---

## 👤 Profile

* **Candidate:** Abdul Wahab Saim
* **Primary Certification:** Cisco Certified Network Associate (CCNA 200-301)
* **Professional Links:**
  * **GitHub:** [github.com/abdulwahabsaim](https://github.com/abdulwahabsaim)
  * **Live Portfolio Website:** [abdulwahabsaim.github.io](https://abdulwahabsaim.github.io)
  * **LinkedIn Profile:** [linkedin.com/in/abdulwahabsaim](https://www.linkedin.com/in/abdulwahabsaim/)

---
