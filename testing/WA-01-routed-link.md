# Test WA-01 — Direct routed link connectivity

Date: 2026-11-20 (local time)

| Test | Expected | Observed |
| --- | --- | --- |
| Routed port mode (CORE-01) | Switchport disabled | Confirmed by user CLI output |
| CORE-01 Gi0/1 | 10.10.250.1, up/up | Confirmed in screenshot |
| DSW-01 Gi0/1 | 10.10.250.2, up/up | Confirmed in screenshot |
| DSW-01 ping CORE-01 | ICMP replies from 10.10.250.1 | Success reported by user; corrected ping screenshot pending |

Correct command on WA-DSW-01 in configuration mode:

```text
do ping 10.10.250.1
```

Earlier screenshots show successful self-pings (CORE-01 to .1 and DSW-01 to .2), which do not validate peer connectivity. Those were corrected during the lab. Do not attribute their 5/5 results or latency to the peer test.

Status: interface checks verified; remote ping passed as reported, screenshot pending. No multi-hop routing or failover tests performed.
