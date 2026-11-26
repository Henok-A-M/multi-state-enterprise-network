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
WA-DSW-02 was subsequently inspected. It is confirmed as VLAN 10 root bridge, with Root ID equal to Bridge ID (priority 32778, MAC 0001.43C9.5CCD); IOS explicitly states `This bridge is the root`. Its Fa0/1 is Designated/FWD, cost 19. Next inspect WA-DSW-01 STP VLAN 10 before choosing priority changes or Layer 2 inter-switch design. Distribution/core uplinks are routed Layer 3 links, so both ASW links forwarding does not establish redundant VLAN gateway behavior or prove a loop-free campus interconnection. Do not infer Layer 2 resilience solely from two links showing trunking or forwarding.

The Step 56 and Step 57 screenshots were reviewed in chat but have not yet been added to the GitHub screenshot gallery.

## Step 58 — WA-DSW-01 verified

Read-only `do show spanning-tree vlan 10` screenshot showed Root ID priority 32778, MAC 0001.43C9.5CCD (same VLAN 10 root previously verified on WA-DSW-02), cost 38, root port Fa0/1. Local Bridge ID priority 32778 and MAC 0030.F2B6.B95D; Fa0/1 has role Root, state FWD, port cost 19. With the known physical cabling, DSW-01 currently reaches the DSW-02 root over its Fa0/1 through ASW-01 and the ASW-01→DSW-02 link. This uses the access switch as Layer 2 transit and is not the desired final distribution design. No STP priorities or direct inter-distribution link configured yet. Next: plan/control primary/secondary VLAN root priorities, then add and validate a direct Layer 2 distribution trunk and STP blocking behavior. Step 58 screenshot has not yet been uploaded.

## Step 59 — Intentional VLAN 10 root election on WA-DSW-01

Configured on WA-DSW-01 global configuration mode:

```text
spanning-tree vlan 10 priority 4096
do show spanning-tree vlan 10
```

Screenshot verified `Root ID Priority 4106`, root MAC `0030.F2B6.B95D`, and the explicit IOS text `This bridge is the root`. Local Bridge ID is also priority 4106; Fa0/1 changed from Root/FWD to Designated/FWD. The effective priority is base 4096 plus VLAN 10 system ID extension. This confirms the intended preferred root on the local switch; root convergence on other switches should be checked separately. Backup STP priority on WA-DSW-02 and a direct DSW-to-DSW Layer 2 connection remain pending. Original screenshot has not yet been uploaded to GitHub.

## Step 60 — Secondary root priority set and verified on WA-DSW-02

Applied `spanning-tree vlan 10 priority 8192` to WA-DSW-02. The follow-up `do show spanning-tree vlan 10` screenshot confirms:

- Root ID priority 4106 and MAC 0030.F2B6.B95D: WA-DSW-01 remains the root.
- Local Bridge ID priority 8202 (8192 + VLAN 10 extension) and MAC 0001.43C9.5CCD.
- Root path cost 38, Fa0/1 Root/FWD, port cost 19, still reaching the root through WA-ASW-01.

This validates the intentional primary/secondary root order for VLAN 10 only. Remaining VLAN priorities, physical access resiliency, and a direct inter-distribution Layer 2 trunk are not implemented or tested. Screenshot reviewed in chat but not uploaded to GitHub.
