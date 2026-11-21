# Washington core-to-distribution routed infrastructure

Status: all four direct links configured and tested in Packet Tracer 9.0.1. Multi-hop routing and failover are not yet validated.

| Link | Subnet | Core interface / IP | Distribution interface / IP |
| --- | --- | --- | --- |
| WA-01 | 10.10.250.0/30 | CORE-01 Gi0/1 — 10.10.250.1 | DSW-01 Gi0/1 — 10.10.250.2 |
| WA-02 | 10.10.250.4/30 | CORE-01 Gi0/2 — 10.10.250.5 | DSW-02 Gi0/2 — 10.10.250.6 |
| WA-03 | 10.10.250.8/30 | CORE-02 Gi0/2 — 10.10.250.9 | DSW-01 Gi0/2 — 10.10.250.10 |
| WA-04 | 10.10.250.12/30 | CORE-02 Gi0/1 — 10.10.250.13 | DSW-02 Gi0/1 — 10.10.250.14 |

All ports use routed mode (no switchport), mask 255.255.255.252, and no shutdown. IP routing enabled on all four multilayer switches. The confirmed CORE-02 CDP port mapping differed from the initial plan; addressing was adjusted to match actual cabling.

Both GigabitEthernet ports on each multilayer switch are occupied. Additional future connections must use available FastEthernet ports or a different simulated device model; this is a simulation constraint.

See [validation](../testing/WA-core-distribution-validation.md).
