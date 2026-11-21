# WA — OSPF functional validation

## Baseline and post-implementation test

Source device: WA-CORE-01. Destination: 10.10.250.14 (DSW-02 Gi0/1, remote subnet 10.10.250.12/30).

| Phase | ICMP result |
| --- | --- |
| Before OSPF | 0/5 (0%) |
| After OSPF on all four switches | 5/5 (100%), RTT 0/0/0 ms |

Both tests appear in the same final CORE-01 CLI screenshot. This validates routing to a non-directly-connected subnet; it does not by itself validate alternate-path recovery.

## Neighbor and route evidence

- DSW-01: neighbor 1.1.1.1 at 10.10.250.1 via Gi0/1, FULL/DR.
- CORE-02: neighbor 1.1.1.3 at 10.10.250.10 via Gi0/2, FULL/DR.
- DSW-02: neighbors 1.1.1.2 at 10.10.250.13 via Gi0/1 and 1.1.1.1 at 10.10.250.5 via Gi0/2, both FULL/DR in repeated complete outputs.
- CORE-01: adjacency log confirms both 1.1.1.3 and 1.1.1.4 reached FULL.
- DSW-01 learned 10.10.250.4/30 through OSPF, with administrative distance 110 and metric 2, next hop 10.10.250.1 via Gi0/1.

Screenshot evidence reviewed in lab session; original image files not uploaded to GitHub. Next: inspect baseline routes and run a controlled link-failure test, then restore link and verify recovery.
