# WA-02 — Wrong-device configuration and recovery

## Incident
While preparing the CORE-02 to DSW-01 link, commands intended for WA-DSW-01 were entered on WA-CORE-01. Gi0/2 was changed from 10.10.250.5/30 to 10.10.250.10/30. The screenshot shows up/up interfaces but a failed ping to 10.10.250.9 (0/5). The physical peer on Gi0/2 is WA-DSW-02 at 10.10.250.6, so the accidental change put the adjacent interfaces in different subnets.

## Recovery
On WA-CORE-01:
```text
configure terminal
interface gigabitEthernet 0/2
ip address 10.10.250.5 255.255.255.252
end
ping 10.10.250.6
```
Initial recovery ping: 80% reported. Repeat ping: user confirmed success. ARP resolution is a possible explanation for the initial loss, not independently proven. The incident and earlier successful peer ping screenshots are linked below; a separate recovery screenshot is not available.

## Prevention
Confirm IOS hostname and target interface before any configuration change. Compare with the port/IP map and verify peer connectivity after changes. A link being up/up does not establish correct IP addressing.

## Visual evidence

- [05-WA-wrong-device-IP-incident](../screenshots/05-WA-wrong-device-IP-incident.png)
- [03-WA-02-peer-ping](../screenshots/03-WA-02-peer-ping.png)

[Complete screenshot index](../screenshots/README.md)
