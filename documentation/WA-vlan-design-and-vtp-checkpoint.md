# Washington VLAN design and VTP checkpoint — Step 47

## Approved addressing plan

| VLAN | Name | Intended subnet |
| --- | --- | --- |
| 10 | ENGINEERING | 10.10.10.0/24 |
| 20 | OPERATIONS | 10.10.20.0/24 |
| 30 | HR | 10.10.30.0/24 |
| 40 | FINANCE | 10.10.40.0/24 |
| 50 | IT_ADMIN | 10.10.50.0/24 |
| 60 | SERVERS | 10.10.60.0/24 |
| 70 | GUEST | 10.10.70.0/24 |
| 99 | MANAGEMENT | 10.10.99.0/24 |
| 999 | NATIVE_UNUSED | None |

All nine VLANs created and shown active in WA-DSW-02 CLI output (show vlan brief). No endpoint ports assigned to these VLANs yet. Subnets are planned; no SVIs or default gateways configured for them. VLAN 999 has been created but is not yet configured as the native VLAN on trunks.

## VTP inspection — WA-ASW-01

Commands executed: show vlan brief; show vtp status.

Observed results:
- VTP version 1, operating mode Server, empty domain name.
- Configuration revision 0; five existing VLANs (1, 1002–1005).
- Pruning disabled; VTP V2 mode disabled.
- Nine departmental/design VLANs on DSW-02 are not present on ASW-01.

## Proposed design — not implemented

Use VTP Transparent mode on participating Layer 2 switches, with explicitly managed local VLAN databases, to reduce the risk of unintended automatic database changes. Transparent mode does not automatically apply received VLAN updates; it may forward VTP messages depending on version and configuration. No VTP setting has been changed during this checkpoint.

## Resume instructions

Step 48 remains pending. On WA-ASW-01, currently at privileged EXEC prompt, enter:
```text
configure terminal
vtp mode transparent
do show vtp status
```
Verify the operating mode is Transparent before proceeding. Inspect and configure VTP policy on both distribution switches, verify local VLAN databases, create missing VLANs where required, then implement controlled trunk VLAN lists, native VLAN consistency, STP, SVIs and HSRP. VLAN propagation, tagged endpoint traffic and Layer 2 failover have not been validated.

## Persistence and evidence

Core and distribution routing configurations were saved at the previous milestone. Saving subsequent trunk and VLAN changes has not yet been confirmed. Selected CLI screenshots are uploaded and linked below. The Packet Tracer project file is still pending.

## Visual evidence

- [20-WA-DSW-02-VLAN-database](../screenshots/20-WA-DSW-02-VLAN-database.png)
- [21-WA-ASW-01-VTP-baseline](../screenshots/21-WA-ASW-01-VTP-baseline.png)

[Complete screenshot index](../screenshots/README.md)
