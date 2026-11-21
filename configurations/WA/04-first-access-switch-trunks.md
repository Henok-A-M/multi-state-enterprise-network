# WA — First dual-uplink access switch

## Hardware decision
Retain the existing Cisco 2950-24 access switches for the functional Packet Tracer lab. A test 2950T-24 showed 24 FastEthernet and two GigabitEthernet ports, but all GigabitEthernet ports on the existing 3560 distribution switches are occupied by routed core links. Access uplinks therefore use FastEthernet. This is a simulation constraint, not a production bandwidth recommendation. Ten 24-port switches with two uplinks each leave 220 endpoint-facing ports; the simulated topology represents the planned 300-user headquarters rather than providing full physical capacity.

## Pilot cabling
Copper crossover; cabling confirmed by user.

| Distribution endpoint | Access endpoint |
| --- | --- |
| WA-DSW-01 Fa0/1 | WA-ASW-01 Fa0/23 |
| WA-DSW-02 Fa0/1 | WA-ASW-01 Fa0/24 |

## Configuration
On each distribution Fa0/1: switchport trunk encapsulation dot1q, switchport mode trunk, no shutdown.
On WA-ASW-01 Fa0/23 and Fa0/24: switchport mode trunk, no shutdown. IOS hostname WA-ASW-01 configured.

## Observed validation
CLI screenshots on all three switches show the four endpoints in mode on, encapsulation 802.1Q, status trunking. Native VLAN 1, allowed VLANs 1–1005; VLAN 1 is the only active and forwarding VLAN listed. Before explicit configuration, access Fa0/24 showed desirable mode and negotiated 802.1Q, demonstrating DTP behavior. Endpoint identity mapping not yet independently checked with CDP.

## Next steps
The departmental VLAN design is approved and nine VLANs are created on WA-DSW-02. See [VLAN and VTP checkpoint](../../documentation/WA-vlan-design-and-vtp-checkpoint.md). VTP mode is unchanged; resume at Step 48. Validate tagged traffic, configure STP roots and redundant gateways, restrict allowed VLANs and harden DTP/native VLAN where supported. Only the first access switch is cabled and tested; no departmental VLAN traffic or access-layer failover tests yet. Screenshots reviewed in chat but not uploaded.
