# Project journal

## 2026-11-20 — Project initiation

Defined the initial scope: a fictional three-state enterprise with Washington headquarters and California and Texas branches. Next: establish requirements, select a simulation platform and draft the network architecture. Implementation has not started.

## 2026-11-20 — Architecture baseline and first routed link

Selected Cisco Packet Tracer 9.0.1. Discussed least privilege, VLANs, ACLs, layered campus design, STP, HSRP, OSPF, full-mesh WAN, IPsec, redundant ISPs/routers, firewall HA, DMZ and centralized services. These are design concepts, not completed deployments.

Placed 14 representative Washington switches and configured the first point-to-point /30 link between WA-CORE-01 and WA-DSW-01. Verified both interfaces up/up and corrected self-ping tests. Corrected peer ping from WA-CORE-01 to WA-DSW-01 verified from the supplied screenshot: 5/5, 100% success. Next: review access-switch models and remaining port budget, complete core/distribution links and enable routing.

See [design baseline](../architecture/enterprise-design.md) and [milestone WA-01](../testing/WA-01-routed-link.md).

## Washington headquarters — Four routed links

Completed the four point-to-point /30 connections between the core and distribution switches. All direct peer links passed ping testing; WA-02 recovery was confirmed by the user after restoring its IP address. CDP revealed reversed CORE-02 port assignments relative to the original design, which were corrected without recabling. See [as-built address map](../documentation/WA-routed-link-map.md) and [test results](../testing/WA-core-distribution-validation.md). Next: configure OSPF and validate multi-hop connectivity and failover. Selected screenshots are uploaded and linked below.

## Washington headquarters — OSPF Area 0

Configured process 1 with four unique router IDs and precise /30 wildcard statements. Observed four FULL adjacencies, an OSPF-learned route on DSW-01 (AD 110, cost 2), and successful remote subnet ping from CORE-01 to 10.10.250.14 (0/5 before OSPF, 5/5 afterward). See [configuration](../configurations/WA/03-ospf-area-zero.md) and [validation](../testing/WA-OSPF-validation.md). Next: verify baseline route and test alternate-path recovery. Selected screenshots are uploaded and linked below.

## Washington headquarters — OSPF failover and recovery

Intentionally disabled CORE-01 Gi0/2, observed neighbor 1.1.1.4 transition from FULL to DOWN, and verified alternate route cost 3 via 10.10.250.2. Ping to 10.10.250.14 succeeded 5/5 after convergence. Restored the interface, observed adjacency return to FULL and the original cost 2 route via 10.10.250.6 return automatically. See [test record](../testing/WA-OSPF-failover-recovery.md). Exact convergence time and continuous packet loss not measured. Final recovery ping verified 5/5 (100%), RTT 0/0/0 ms, after the cost 2 route returned. User confirmed saving startup configurations on all four multilayer switches and saving the Packet Tracer project. Next: access-layer design and implementation.

## Washington headquarters — Access-layer pilot and VLAN checkpoint

Retained the 2950-24 access switches due to distribution Gigabit port constraints. Connected WA-ASW-01 to both distribution switches using FastEthernet and explicitly configured all four trunk endpoints; CLI showed 802.1Q trunking, native VLAN 1, allowed range 1–1005. Approved VLANs 10–70 (increments of 10), 99 and 999. Created and verified all nine on WA-DSW-02. Inspected WA-ASW-01: VTP v1 Server, no domain, revision 0, five default VLANs only. Proposed Transparent mode but user stopped before applying it. Resume at Step 48 on WA-ASW-01. New trunk/VLAN configuration saves not yet confirmed. See [checkpoint](../documentation/WA-vlan-design-and-vtp-checkpoint.md) and [trunk record](../configurations/WA/04-first-access-switch-trunks.md).

## Visual evidence

- [12-WA-OSPF-before-after](../screenshots/12-WA-OSPF-before-after.png)
- [13-WA-OSPF-failover](../screenshots/13-WA-OSPF-failover.png)
- [14-WA-OSPF-recovery](../screenshots/14-WA-OSPF-recovery.png)
- [20-WA-DSW-02-VLAN-database](../screenshots/20-WA-DSW-02-VLAN-database.png)
- [21-WA-ASW-01-VTP-baseline](../screenshots/21-WA-ASW-01-VTP-baseline.png)

[Complete screenshot index](../screenshots/README.md)
