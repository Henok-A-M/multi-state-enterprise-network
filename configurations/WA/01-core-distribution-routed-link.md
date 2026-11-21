# WA-01 — First routed core-to-distribution link

Date: 2026-11-20 (local time)
Platform: Cisco Packet Tracer 9.0.1

## Objective

Establish a point-to-point Layer 3 link between WA-CORE-01 and WA-DSW-01 instead of extending a Layer 2 broadcast domain into the core.

| Device | Port | Address | Mask |
| --- | --- | --- | --- |
| WA-CORE-01 | Gi0/1 | 10.10.250.1 | 255.255.255.252 |
| WA-DSW-01 | Gi0/1 | 10.10.250.2 | 255.255.255.252 |

Subnet: 10.10.250.0/30. Network address .0, usable addresses .1 and .2, broadcast .3. Copper crossover cable used in Packet Tracer.

## Configured commands

WA-CORE-01:

```text
enable
configure terminal
hostname WA-CORE-01
interface gigabitEthernet 0/1
no switchport
ip address 10.10.250.1 255.255.255.252
no shutdown
```

WA-DSW-01:

```text
enable
configure terminal
hostname WA-DSW-01
interface gigabitEthernet 0/1
no switchport
ip address 10.10.250.2 255.255.255.252
no shutdown
```

## Verification

Screenshots supplied during the lab show Switchport: Disabled on CORE-01 (reported CLI output), and both Gi0/1 interfaces up/up with their respective IP addresses. The user reported a successful ping from WA-DSW-01 to 10.10.250.1 after correcting earlier self-ping tests. A subsequent screenshot confirms the reverse peer test from WA-CORE-01 to 10.10.250.2: 5/5 replies, 100% success. See [test record](../../testing/WA-01-routed-link.md).

IP routing across multiple subnets and OSPF have not yet been implemented or tested. Saving startup configurations was instructed but not confirmed.

## Visual evidence

- [02-WA-01-peer-ping](../../screenshots/02-WA-01-peer-ping.png)

[Complete screenshot index](../../screenshots/README.md)
