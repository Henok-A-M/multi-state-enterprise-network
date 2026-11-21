# WA-02 — CORE-01 to DSW-02

| Device | Interface | Address |
| --- | --- | --- |
| WA-CORE-01 | Gi0/2 | 10.10.250.5/30 |
| WA-DSW-02 | Gi0/2 | 10.10.250.6/30 |

Both interfaces configured with no switchport, mask 255.255.255.252. IP routing enabled on both devices. Both interfaces verified up/up in screenshots. CORE-01 routing table showed connected networks 10.10.250.0/30 and 10.10.250.4/30. Ping from CORE-01 to .6 initially 4/5, then 5/5 (screenshot verified). A later accidental IP change was corrected; recovery confirmed by user. See [incident record](../../troubleshooting/WA-02-wrong-device-configuration.md).

CORE-02 CDP output also established actual port mapping: Gi0/1 to DSW-02 Gi0/1, Gi0/2 to DSW-01 Gi0/2. CORE-02 now has .13/30 and .9/30 on these respective ports, both up/up; peer configuration and ping tests pending.
