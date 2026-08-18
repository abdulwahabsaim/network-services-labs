<div align="center">

# 🌐 Core Network Services & Infrastructure Labs

[![Domain](https://img.shields.io/badge/Domain-Core_Network_Services-00599C?style=for-the-badge&logo=cisco&logoColor=white)](https://cisco.com)
[![Protocols](https://img.shields.io/badge/Protocols-DHCP_|_DNS_|_HTTP_|_HTTPS-brightgreen?style=for-the-badge)]()
[![Platform](https://img.shields.io/badge/Platform-Cisco_Catalyst_2960_/_Multi--Server-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white)](https://cisco.com)
[![Status](https://img.shields.io/badge/Portfolio_Status-Verified-success?style=for-the-badge)]()

<p align="center">
  <b>A dedicated hands-on portfolio showcasing the deployment, integration, and verification of core application-layer services: DHCP dynamic addressing (D.O.R.A), DNS authoritative name resolution, and HTTP/HTTPS web application delivery.</b>
</p>

</div>

---

## 📌 Executive Overview

Every enterprise IT environment depends on core network services to enable client communication. Without automated dynamic addressing and name resolution, modern network hosts cannot locate internal services, cloud endpoints, or web applications.

This repository demonstrates the complete **End-to-End Client Lifecycle Workflow**:
1. **Dynamic Addressing:** Automated address provisioning via **DHCP (UDP 67/68)**.
2. **Name Resolution:** Translating human-readable domain names into IP addresses via **DNS (UDP 53)**.
3. **Application Delivery:** Serving web applications over **HTTP/HTTPS (TCP 80/443)**.

---

## 🗺️ Master Lab Catalog & Navigation

| Lab Directory | Topic & Service Architecture | Integrated Protocols | Key Verification Highlights |
| :--- | :--- | :--- | :--- |
| [**`01-core-network-services-dhcp-dns-http`**](./01-core-network-services-dhcp-dns-http) | Multi-Server Infrastructure Lifecycle | DHCP (D.O.R.A), DNS (A-Record), HTTP Web | `ipconfig /renew`, `nslookup cisco.com`, `ping`, Web Browser rendering |

---

## 🔄 End-to-End Client Initialization Lifecycle

```text
       ┌───────────────┐
       │   Client PC0  │
       └───────┬───────┘
               │
   [1. DHCP Lease Request]
               ├─── DHCP DISCOVER (Broadcast) ───> [ DHCP Server: 192.168.0.101 ]
               │<── DHCP ACK (Lease: .51, DNS: .103) ──┘
               │
   [2. DNS Name Resolution]
               ├─── DNS Query ("cisco.com") ─────> [ DNS Server: 192.168.0.103 ]
               │<── DNS Answer (IP: 192.168.0.102) ───┘
               │
   [3. Web Page Retrieval]
               ├─── HTTP GET / (TCP 80) ─────────> [ Web Server: 192.168.0.102 ]
               │<── HTTP 200 OK (HTML Payload) ───────┘
```

---

## 🧰 Master Network Services CLI Verification Cheat Sheet

| Diagnostic Tool / Command | Operating Level | Purpose & Expected Output |
| :--- | :--- | :--- |
| `ipconfig` / `ipconfig /all` | Host OS | Displays dynamic IPv4 lease, subnet mask, default gateway, and learned DNS server IP. |
| `ipconfig /renew` | Host OS | Forces the client adapter to release its active lease and renegotiate a fresh DHCP D.O.R.A exchange. |
| `nslookup <domain>` | Host OS | Queries the configured DNS server to verify A-record resolution and DNS server response time. |
| `ping <domain>` | Host OS | Tests Layer 3 reachability while verifying that OS-level DNS resolution occurs automatically prior to ICMP transmission. |
| `show mac address-table` | Switch CLI (`#`) | Displays active Layer 2 forwarding entries mapped to the server and client physical switchports. |

---

## 📂 Repository File Structure

```text
network-services-labs/
├── README.md                                  <-- Master Repository Index
└── 01-core-network-services-dhcp-dns-http/
    ├── README.md                              (Lab Documentation & D.O.R.A Workflow)
    ├── topology.png                           (Network Architecture Diagram)
    ├── core-network-services.pkt              (Packet Tracer Simulation File)
    └── switch-config.ios                      (Layer 2 Catalyst 2960 Switch Config)
