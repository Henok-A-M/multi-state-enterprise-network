# Project journal

## 2026-11-20 — Project initiation

Defined the initial scope: a fictional three-state enterprise with Washington headquarters and California and Texas branches. Next: establish requirements, select a simulation platform and draft the network architecture. Implementation has not started.

## 2026-11-20 — Architecture baseline and first routed link

Selected Cisco Packet Tracer 9.0.1. Discussed least privilege, VLANs, ACLs, layered campus design, STP, HSRP, OSPF, full-mesh WAN, IPsec, redundant ISPs/routers, firewall HA, DMZ and centralized services. These are design concepts, not completed deployments.

Placed 14 representative Washington switches and configured the first point-to-point /30 link between WA-CORE-01 and WA-DSW-01. Verified both interfaces up/up and corrected self-ping tests. Corrected peer ping from WA-CORE-01 to WA-DSW-01 verified from the supplied screenshot: 5/5, 100% success. Next: review access-switch models and remaining port budget, complete core/distribution links and enable routing.

See [design baseline](../architecture/enterprise-design.md) and [milestone WA-01](../testing/WA-01-routed-link.md).
