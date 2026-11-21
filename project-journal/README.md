# Project journal

## 2026-11-20 — Project initiation

Defined the initial scope: a fictional three-state enterprise with Washington headquarters and California and Texas branches. Next: establish requirements, select a simulation platform and draft the network architecture. Implementation has not started.

## 2026-11-20 — Architecture baseline and first routed link

Selected Cisco Packet Tracer 9.0.1. Discussed least privilege, VLANs, ACLs, layered campus design, STP, HSRP, OSPF, full-mesh WAN, IPsec, redundant ISPs/routers, firewall HA, DMZ and centralized services. These are design concepts, not completed deployments.

Placed 14 representative Washington switches and configured the first point-to-point /30 link between WA-CORE-01 and WA-DSW-01. Verified both interfaces up/up and corrected self-ping tests. Corrected peer ping from WA-CORE-01 to WA-DSW-01 verified from the supplied screenshot: 5/5, 100% success. Next: review access-switch models and remaining port budget, complete core/distribution links and enable routing.

See [design baseline](../architecture/enterprise-design.md) and [milestone WA-01](../testing/WA-01-routed-link.md).

## Washington headquarters — Four routed links

Completed the four point-to-point /30 connections between the core and distribution switches. All direct peer links passed ping testing; WA-02 recovery was confirmed by the user after restoring its IP address. CDP revealed reversed CORE-02 port assignments relative to the original design, which were corrected without recabling. See [as-built address map](../documentation/WA-routed-link-map.md) and [test results](../testing/WA-core-distribution-validation.md). Next: configure OSPF and validate multi-hop connectivity and failover. Original screenshots remain to be uploaded.

## Washington headquarters — OSPF Area 0

Configured process 1 with four unique router IDs and precise /30 wildcard statements. Observed four FULL adjacencies, an OSPF-learned route on DSW-01 (AD 110, cost 2), and successful remote subnet ping from CORE-01 to 10.10.250.14 (0/5 before OSPF, 5/5 afterward). See [configuration](../configurations/WA/03-ospf-area-zero.md) and [validation](../testing/WA-OSPF-validation.md). Next: verify baseline route and test alternate-path recovery. Original screenshots not uploaded.

## Washington headquarters — OSPF failover and recovery

Intentionally disabled CORE-01 Gi0/2, observed neighbor 1.1.1.4 transition from FULL to DOWN, and verified alternate route cost 3 via 10.10.250.2. Ping to 10.10.250.14 succeeded 5/5 after convergence. Restored the interface, observed adjacency return to FULL and the original cost 2 route via 10.10.250.6 return automatically. See [test record](../testing/WA-OSPF-failover-recovery.md). Exact convergence time and continuous packet loss not measured. Final recovery ping and configuration persistence pending.
