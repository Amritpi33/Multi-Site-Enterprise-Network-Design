# CPNT300 – Multi-Site Enterprise Network Design

## Overview
This project was part of **CPNT300** and focused on designing a logical and scalable network for a local hardware company.  
- **Sites:** Headquarters (Site 1), Site 2, Site 3, and a Data Centre.  
- **Architecture:** Three-tier hierarchical design with Core, Distribution, and Access layers.  
- **Routing Protocols:** OSPF (HQ, Site 3, Data Centre) and EIGRP (Site 2).  
- **Redundancy:** HSRP for HQ gateways, redundant Core switches.  
- **Data Centre Services:** DHCP, DNS, RADIUS, FTP, multiple Web servers.  
- **Wireless:** WLAN controller with WPA2-Enterprise Employee WLAN and WPA2-PSK Guest WLAN.  
- **External Connectivity:** Edge router to ISP (200.200.200.0/30), ISP server subnet 200.200.200.8/29.

## Subnetting & Summarization
- Site 1 summary: `10.25.0.0/20`
- Site 2 summary: `10.25.16.0/22`
- Site 3 summary: `10.25.32.0/26`
- Data Centre summary: `10.25.40.0/22`

See full details in [`addressing/`](addressing).

## DHCP Plan
Central DHCP server at Data Centre. Pools configured for all VLANs:
- VLAN10 (HQ LAN1) → 10.25.0.0/21
- VLAN20 (HQ LAN2) → 10.25.8.0/23
- VLAN30 (HQ LAN3) → 10.25.10.0/23
- VLAN40 (HQ LAN4) → 10.25.12.0/24
- VLAN50–80 (Site2 LANs) → 10.25.16.0/23 → 10.25.19.128/26
- VLAN90 (Site3) → 10.25.32.0/26
- VLAN100 (Servers) → 10.25.40.0/28
- VLAN200 (Employee WLAN) → 10.25.41.0/24
- VLAN300 (Guest WLAN) → 10.25.42.0/24

## WLAN Table
- **Employee WLAN** → WPA2-Enterprise, usernames: `employee1/2/3`, unique passwords.
- **Guest WLAN** → WPA2-PSK, SSID `WLAN-GUEST`, password `GuestPass2024!`.

## Artifacts
- [Packet Tracer File](pkt/cpnt300_network_design.pkt)
- [Subnetting Plans](addressing/)
- [Device IP Plan](addressing/device-ip-plan.csv)
- [DHCP Plan](addressing/dhcp-plan.csv)
- [WLAN Plan](addressing/wlan-plan.csv)
- [Site Topology](topology/site-topology.png)
- [Data Centre + ISP Topology](topology/datacenter-topology.png)

## Lessons Learned
- Designed hierarchical 3-tier networks with redundancy (HSRP, dual core).  
- Applied VLSM + summarization per site.  
- Mixed routing protocols (EIGRP + OSPF).  
- Centralized DHCP with IP helper addresses.  
- Configured WLANs for enterprise and guest users.  
