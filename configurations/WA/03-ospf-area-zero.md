# WA — OSPF Area 0 implementation

Cisco Packet Tracer 9.0.1; four multilayer switches, IP routing enabled, four /30 transit networks. OSPF process 1 is local to each device. All transit interfaces participate in area 0.

| Device | Router ID | Network statements (each wildcard 0.0.0.3, area 0) |
| --- | --- | --- |
| WA-CORE-01 | 1.1.1.1 | 10.10.250.0, 10.10.250.4 |
| WA-CORE-02 | 1.1.1.2 | 10.10.250.8, 10.10.250.12 |
| WA-DSW-01 | 1.1.1.3 | 10.10.250.0, 10.10.250.8 |
| WA-DSW-02 | 1.1.1.4 | 10.10.250.4, 10.10.250.12 |

Example on CORE-01:
```text
router ospf 1
 router-id 1.1.1.1
 network 10.10.250.0 0.0.0.3 area 0
 network 10.10.250.4 0.0.0.3 area 0
```

All four configurations observed in CLI screenshots. Ethernet broadcast network type retained, with DR/BDR election. Four adjacencies observed reaching FULL. See [validation](../../testing/WA-OSPF-validation.md). Failover testing, configuration persistence, and routing security hardening remain pending.
