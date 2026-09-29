Multi-Site Enterprise Network — Cisco Packet Tracer Lab

A simulated enterprise network built in Cisco Packet Tracer, designed to demonstrate core network engineering concepts: VLAN segmentation, inter-VLAN routing, WAN connectivity, and dynamic routing across multiple sites.

Overview

The network consists of a headquarters (HQ) office and two branch offices, connected over simulated WAN links, with OSPF handling dynamic routing between all three sites. Each site uses VLANs to segment traffic by department/purpose, with a router-on-a-stick configuration providing inter-VLAN routing.

<img width="1917" height="1078" alt="Screenshot 2026-09-14 215521" src="https://github.com/user-attachments/assets/13653650-7851-458f-af07-53d507d87e57" />

Topology
HQ: 1 router, 1 switch, 3 VLANs (Staff, Servers, Guest), 2 PCs + 1 server
Branch1: 1 router, 1 switch, 2 VLANs (Staff, Guest), 2 PCs
Branch2: 1 router, 1 switch, 2 VLANs (Staff, Guest), 2 PCs
WAN: HQ connects directly to both branches via point-to-point serial links (hub-and-spoke)
Routing: OSPF (Area 0) across all three sites
IP Addressing Scheme
Site	VLAN	Network	Purpose
HQ	VLAN 10 (Staff)	10.10.10.0/24	Employee PCs
HQ	VLAN 20 (Servers)	10.10.20.0/24	Internal servers
HQ	VLAN 30 (Guest)	10.10.30.0/24	Guest access
Branch1	VLAN 10 (Staff)	10.20.10.0/24	Employee PCs
Branch1	VLAN 30 (Guest)	10.20.30.0/24	Guest access
Branch2	VLAN 10 (Staff)	10.30.10.0/24	Employee PCs
Branch2	VLAN 30 (Guest)	10.30.30.0/24	Guest access
WAN	HQ ↔ Branch1	192.168.1.0/30	Point-to-point serial link
WAN	HQ ↔ Branch2	192.168.1.4/30	Point-to-point serial link
Technologies & Concepts Used
VLAN creation and port assignment (access/trunk)
Router-on-a-stick (802.1Q subinterfaces) for inter-VLAN routing
Point-to-point WAN links (serial DCE/DTE)
OSPF (single area) for dynamic inter-site routing
IP subnetting and addressing design
Cisco IOS CLI configuration and verification (show ip interface brief, show vlan brief, show ip ospf neighbor)
Verification
Inter-VLAN routing confirmed: devices in different VLANs at HQ can reach each other only through the router.
Inter-site connectivity confirmed: PCs at HQ can successfully ping devices at both Branch1 and Branch2 across OSPF-routed paths (verified via ping and TTL hop count).
OSPF neighbor adjacencies confirmed FULL between HQ and both branches via show ip ospf neighbor.
Challenges & Troubleshooting

Documenting real issues encountered, since debugging is as much a part of network engineering as the initial design:

Router config loss on power cycle: Adding a WIC/HWIC serial module requires powering off the router. Since running-config hadn't been saved to startup-config, this wiped VLAN subinterface configuration on HQ and both branch routers. Fixed by rebuilding the configs and adopting copy running-config startup-config as a standard step after every configuration change.
OSPF/serial link not coming up: One WAN link stayed down despite correct IP addressing and clock rate configuration. Diagnosed using show controllers , which revealed the cable was actually connected to the wrong physical port. Re-cabled to the correct interface, resolving the issue.
Cabling mix-up between branches: A WAN link intended to connect HQ to Branch2 was accidentally cabled between Branch1 and Branch2 instead, due to router proximity in the topology view. Identified by clicking the cable in the topology to confirm actual endpoints, then corrected.
Files in This Repository
topology-diagram.png — Full network topology screenshot
Intervlan.pkt — Cisco Packet Tracer project file
configs/ — Full show running-config output for each router and switch

Author

Built as a hands-on learning project while studying for CCNA and preparing for entry-level network engineering roles.
