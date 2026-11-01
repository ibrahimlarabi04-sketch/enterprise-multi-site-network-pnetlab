# Network Design Notes

## Overview

This PNETLab exercise models a multi-site enterprise network with a routed core, access networks, VLAN-based segmentation, and redundant external connectivity.

## Main design elements

- **Routing:** Multi-Area OSPF is used for dynamic routing. RIP is used in a separate routing segment and routes are redistributed into OSPF. Static routes are also used for selected network segments.
- **Gateway availability:** HSRP provides virtual default gateways for VLANs. IP SLA tracking is used to monitor reachability and support route/gateway failover behavior.
- **WAN edge:** Two simulated ISP paths provide an opportunity to test primary/backup connectivity.
- **LAN switching:** VLANs and inter-VLAN routing provide segmentation and communication between local networks. EtherChannel was configured using LACP and PAgP.
- **Addressing:** VLSM is used to allocate subnets according to link and LAN requirements.
- **Translation:** NAT/PAT provides address translation for outbound connectivity.

## Current evidence

The repository currently contains screenshots for:
- HSRP state verification
- IP SLA tracking status
- Successful VPCS connectivity test to 8.8.8.8
- OSPF database in Area 0

## Suggested future additions

- Exported configurations for the routers and switches
- `show ip ospf neighbor` and `show ip route` outputs
- `show etherchannel summary` output
- Before/after screenshots for HSRP and ISP failover tests
- A complete IP addressing table
