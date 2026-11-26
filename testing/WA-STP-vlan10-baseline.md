# WA — Spanning Tree VLAN 10 baseline (Step 56)

## Context
After creating nine VLANs on WA-ASW-01 and verifying Fa0/23 and Fa0/24 trunks, we inspected VLAN 10 Spanning Tree Protocol using `do show spanning-tree vlan 10`. This is a read-only baseline; no STP priorities have been changed.

## Observed output

| Field | CLI result |
| --- | --- |
| VLAN instance | VLAN0010 |
| Protocol | IEEE |
| Root bridge priority | 32778 |
| Root bridge MAC | 0001.43C9.5CCD |
| Root path cost | 19 |
| Local root port | Fa0/24 |
| Root hello / max-age / forward delay | 2 / 20 / 15 seconds |
| Local bridge priority | 32778 (32768 + VLAN 10 extended system ID) |
| Local bridge MAC | 0001.C9D7.6A60 |
| Fa0/24 | Root, forwarding (FWD), cost 19 |
| Fa0/23 | Designated (Desg), forwarding (FWD), cost 19 |

## Interpretation
The local bridge is not the root because its Bridge ID differs from the Root ID. The lowest-cost route from WA-ASW-01 toward the root uses Fa0/24, cabled toward WA-DSW-02. That does not independently prove WA-DSW-02 is the root: verify its own STP Root ID/Bridge ID output. Fa0/23 is designated and also forwarding. No blocked port is visible on ASW-01 for VLAN 10; there may not be a closed Layer 2 loop in this pilot topology.

## Next
Run `do show spanning-tree vlan 10` on WA-DSW-02 (or `show spanning-tree vlan 10` from privileged EXEC) to identify the root bridge. Inspect DSW-01 as needed before configuring bridge priorities, STP modes or access-layer failover. Do not infer Layer 2 resilience solely from two links showing trunking or forwarding.

The screenshot was reviewed in chat and has not yet been added to the GitHub screenshot gallery.
