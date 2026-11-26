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

## Step 63–64 — Direct distribution trunk connected, root-side STP checked

User confirmed Copper Cross-Over interconnect between WA-DSW-01 Fa0/24 and WA-DSW-02 Fa0/24 after configuring 802.1Q trunk mode on both ends. CLI screenshot from **WA-DSW-01** shows Fa0/24 link and line protocol up, and `do show spanning-tree vlan 10` shows the switch remains VLAN 10 root (priority 4106, MAC 0030.F2B6.B95D). Fa0/1 and Fa0/24 both show Designated/FWD, cost 19; this is normal for the root bridge. The screenshot does **not** establish the blocking state on the access switch. Next: inspect WA-ASW-01 `do show spanning-tree vlan 10` to verify that redundant Layer 2 path is blocked where expected. The new screenshot has not been uploaded to the repository.

## Step 64 — Confirmed STP blocking on first access switch

After the new DSW-01 Fa0/24 ↔ DSW-02 Fa0/24 trunk was connected, a `show spanning-tree vlan 10` screenshot from **WA-ASW-01** showed:

- Root Bridge ID priority 4106, MAC 0030.F2B6.B95D (WA-DSW-01).
- Root path cost 19 via access interface Fa0/23.
- **Fa0/23: Root / FWD**, cost 19, primary path toward DSW-01.
- **Fa0/24: Altn / BLK**, cost 19, redundant path toward DSW-02 blocked by STP.

This verifies that IEEE STP created a loop-free forwarding topology for VLAN 10 after the direct distribution interconnect. It does not yet establish failover behavior, end-to-end application connectivity, or spanning-tree decisions for the other eight VLANs. The user initially attempted `do show` from privileged EXEC mode (invalid) and successfully corrected to `show spanning-tree vlan 10`. Screenshot reviewed in the session; separate upload not yet performed.

**Next:** controlled failover test. On WA-ASW-01, shut the root-path interface Fa0/23 only, then verify STP reconverges and Fa0/24 moves to Root/FWD. Restore Fa0/23 afterward and confirm normal roles return. Record observed status; do not claim uninterrupted service without packet monitoring.

## Step 65 — STP uplink failover observed (WA-ASW-01)

User administratively shut down WA-ASW-01 Fa0/23, the original Root/FWD access-to-DSW-01 uplink. Initial `do show spanning-tree vlan 10` screenshot showed the remaining Fa0/24 in Root/LRN (learning), not yet forwarding. A second screenshot after simulation time advanced showed **Fa0/24 Root/FWD**, cost 19 for the port and **root path cost 38** via WA-DSW-02 and the inter-distribution trunk to the unchanged VLAN 10 root WA-DSW-01 (root bridge priority 4106, MAC 0030.F2B6.B95D). This verifies STP changed to the redundant Layer 2 path following a simulated primary-link failure. It does not verify endpoint connectivity, packet loss or convergence duration. **As of this checkpoint WA-ASW-01 Fa0/23 remains administratively down; recovery not yet verified.** Next on WA-ASW-01: `no shutdown` under `interface fastEthernet 0/23`, and recheck `show spanning-tree vlan 10` for preferred Root/FWD on Fa0/23 and Alternate/BLK on Fa0/24. Separate prior incident: WA-DSW-01 Fa0/23 was accidentally shut down in the first attempt; restoration has not been explicitly verified. User screenshots are in the chat but this step's PNGs are not yet uploaded to the repository.

## Step 66 — Primary uplink re-enabled, STP recovery check pending

User entered `no shutdown` on WA-ASW-01 Fa0/23. Screenshot confirms `%LINK-5-CHANGED` interface Fa0/23 changed to up and `%LINEPROTO-5-UPDOWN` line protocol changed to up. However, the `show spanning-tree vlan 10` output visible in the screenshot precedes the `no shutdown` command and still shows Fa0/24 as Root/FWD. **Do not mark STP recovery verified yet.** Next run a fresh `do show spanning-tree vlan 10` on WA-ASW-01 and confirm Fa0/23 Root/FWD and Fa0/24 Altn/BLK after convergence.
