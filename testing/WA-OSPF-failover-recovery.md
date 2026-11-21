# Washington OSPF — Controlled link failure and recovery

## Objective
Validate automatic alternate-path routing and restoration of the preferred route in the four-switch Area 0 topology, Cisco Packet Tracer 9.0.1.

## Test procedure and observed results
Source WA-CORE-01; remote destination 10.10.250.14 on WA-DSW-02 (10.10.250.12/30).

| Phase | Next hop | Exit interface | AD/cost | Ping |
| --- | --- | --- | --- | --- |
| Baseline | 10.10.250.6 | Gi0/2 | 110/2 | 5/5 |
| After Gi0/2 shutdown and convergence | 10.10.250.2 | Gi0/1 | 110/3 | 5/5; RTT 0/0/1 ms |
| After no shutdown and reconvergence | 10.10.250.6 | Gi0/2 | 110/2 | Retest pending |

Commands on WA-CORE-01:
```text
configure terminal
interface gigabitEthernet 0/2
shutdown
do show ip route
do ping 10.10.250.14
no shutdown
do show ip route
```

After shutdown the OSPF log reported neighbor 1.1.1.4 on Gi0/2 changing from FULL to DOWN. The connected 10.10.250.4/30 route disappeared and the alternate OSPF route to 10.10.250.12/30 was installed. Expected alternate forwarding path: CORE-01 → DSW-01 → CORE-02 → DSW-02 (not independently traced).

After no shutdown, the physical interface and protocol returned up. The first routing table still showed cost 3; the adjacency subsequently reached FULL. A repeated routing-table check confirmed:
```text
O 10.10.250.12 [110/2] via 10.10.250.6, 00:00:43, GigabitEthernet0/2
```

All four transit routes were present again. No static routes or manual metric changes were needed.

## Conclusion and limits
Automatic failover and preferred-route restoration verified by CLI screenshots. Ping confirmed reachability after failure convergence, not continuous zero-loss service during transition. Exact convergence duration was not measured. Post-restoration ping and saving configurations remain pending. Original screenshots have not been uploaded.
