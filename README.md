# Enterprise Multi-Site Network – PNETLab

A hands-on enterprise networking project designed, configured, and tested in **PNETLab**. The lab brings together routing, switching, gateway redundancy, WAN connectivity, and network troubleshooting in a multi-site topology.

> **Project scope:** This repository documents the PNETLab lab only.

## Table of Contents

- [Overview](#overview)
- [Network Topology](#network-topology)
- [Architecture Overview](#architecture-overview)
- [Features Implemented](#features-implemented)
- [Addressing and Segmentation](#addressing-and-segmentation)
- [Verification Highlights](#verification-highlights)
- [Repository Structure](#repository-structure)
- [Tools and Technologies](#tools-and-technologies)
- [Future Improvements](#future-improvements)
- [Author](#author)

## Overview

This project simulates a multi-site enterprise network with multiple routers, switches, end devices, and two simulated ISP connections. It was built to practise the design and operation of a resilient network infrastructure.

The lab focuses on integrating dynamic routing, route redistribution, first-hop redundancy, WAN failover mechanisms, VLAN segmentation, and connectivity testing.

## Network Topology

![Enterprise multi-site network topology](topology/network-topology.png)

The topology includes:

- A routed network core interconnecting several network segments.
- LAN segments connected through access switches.
- VLAN-based user networks.
- Remote routed segments.
- Simulated connections to Ooredoo and Algérie Télécom.
- Redundant paths designed to improve network availability.

## Architecture Overview

### Routing architecture

- **OSPF:** Used as the main dynamic routing protocol. The lab includes a multi-area design.
- **OSPF NSSA and RIP redistribution:** The external RIP routing domain is integrated into OSPF through redistribution. The NSSA design uses Type 7 LSAs for external route information.
- **Static routing:** Used for selected network segments and default-route handling.

### LAN and gateway redundancy

- **VLANs:** Separate LAN traffic into logical networks, including VLAN 10 and VLAN 20.
- **Inter-VLAN routing:** Enables communication between permitted VLAN networks.
- **HSRP:** Provides virtual default gateways and Active/Standby gateway redundancy.
- **IP SLA tracking:** Monitors reachability and supports failover decisions when a tracked path becomes unavailable.

### WAN and Internet connectivity

- **Dual-ISP connectivity:** The topology includes Ooredoo and Algérie Télécom as simulated upstream providers.
- **Tracked default routes:** IP SLA monitoring is used with route tracking to support primary/backup path selection.
- **NAT/PAT:** Configured to provide translated outbound connectivity for internal networks.

### Switching and link aggregation

- **Trunking:** Carries VLAN traffic between switching and routing devices where required.
- **EtherChannel:** LACP and PAgP were configured and explored for link aggregation and link redundancy.

## Features Implemented

1. Multi-Area OSPF routing.
2. OSPF NSSA and RIP-to-OSPF route redistribution.
3. Static routing for selected network segments.
4. VLAN segmentation and inter-VLAN routing.
5. HSRP gateway redundancy for VLAN 10 and VLAN 20.
6. IP SLA tracking for reachability monitoring and failover logic.
7. Dual-ISP connectivity using Ooredoo and Algérie Télécom.
8. NAT/PAT for outbound connectivity.
9. VLSM-based IPv4 subnetting.
10. EtherChannel using LACP and PAgP.

## Addressing and Segmentation

The lab uses VLSM to allocate subnets according to the requirements of LAN segments and point-to-point routed links. The topology diagram contains the network prefixes and addressing information used during implementation.

Examples visible in the lab include:

| Network / Purpose | Prefix or address |
|---|---|
| VLAN 10 LAN | `172.16.0.0/22` |
| VLAN 20 LAN | `172.16.4.0/23` |
| Routed point-to-point links | `/30` subnets |
| HSRP virtual gateway for VLAN 10 | `172.16.0.1` |
| HSRP virtual gateway for VLAN 20 | `172.16.2.1` |

The complete per-device addressing table can be added alongside exported device configurations in a future update.

## Verification Highlights

The repository includes real command-line screenshots captured from the PNETLab environment.

| Verification | Evidence |
|---|---|
| HSRP gateway state | [`show standby brief`](screenshots/hsrp-verification.png) displays Active/Standby roles for VLAN subinterfaces and their virtual IP addresses. |
| IP SLA tracking | [`show track`](screenshots/ip-sla-tracking.png) shows both tracked IP SLA operations in an Up state. |
| End-to-end connectivity | [VPCS ping test](screenshots/internet-connectivity.png) shows successful replies from a lab host to `8.8.8.8`. |
| OSPF database | [`show ip ospf database`](screenshots/ospf-database.png) displays OSPF Link-State Database information for Area 0. |

These screenshots document the verification results currently available in the repository. Additional failover and protocol-specific outputs can be added as they are captured.

## Repository Structure

```text
enterprise-multi-site-network-pnetlab/
├── README.md
├── topology/
│   └── network-topology.png
├── screenshots/
│   ├── README.md
│   ├── hsrp-verification.png
│   ├── ip-sla-tracking.png
│   ├── internet-connectivity.png
│   └── ospf-database.png
└── documentation/
    └── network-design.md
```

## Tools and Technologies

- **PNETLab** – network emulation and lab environment.
- **Cisco IOS** – router and switch configuration.
- **VPCS** – end-host connectivity testing.
- **Networking technologies** – OSPF, RIP, HSRP, IP SLA, VLANs, trunking, NAT/PAT, VLSM, EtherChannel, LACP, and PAgP.

## Future Improvements

The project can be extended with additional evidence and documentation:

- Exported router and switch configuration files.
- OSPF neighbor and routing-table verification outputs.
- EtherChannel verification using `show etherchannel summary`.
- Screenshots showing primary-to-backup ISP failover.
- Before-and-after HSRP and IP SLA failover tests.
- A complete IP addressing table for all devices and links.

## Author

**Ibrahim Larabi**
