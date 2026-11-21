# Implementation evidence — Washington

21 relevant screenshots were selected from the actual Packet Tracer session and packaged separately. Full-window captures were cropped to remove the local Windows path from the title bar; CLI and topology evidence were preserved. The PNG files are **pending upload**; the following filenames are an inventory, not links to existing image files. Upload the extracted PNGs into this directory without renaming them. No VTP configuration has been performed.

| Screenshot filename | Evidence | Related documentation |
| --- | --- | --- |
| `01-WA-initial-switch-layout.png` | Initial placement, 14 representative switches; not a completed topology | [Record](../architecture/enterprise-design.md) |
| `02-WA-01-peer-ping.png` | First routed peer ping, 5/5 | [Record](../testing/WA-01-routed-link.md) |
| `03-WA-02-peer-ping.png` | Second peer ping, 5/5 before subsequent address error | [Record](../testing/WA-core-distribution-validation.md) |
| `04-WA-CDP-port-discovery.png` | Actual CORE-02 port mapping | [Record](../troubleshooting/WA-03-cdp-port-mapping.md) |
| `05-WA-wrong-device-IP-incident.png` | Incorrect Gi0/2 address and failed ping | [Record](../troubleshooting/WA-02-wrong-device-configuration.md) |
| `06-WA-03-peer-ping.png` | Third routed peer ping, 5/5 | [Record](../testing/WA-core-distribution-validation.md) |
| `07-WA-04-peer-ping.png` | Fourth routed peer ping, 5/5 | [Record](../testing/WA-core-distribution-validation.md) |
| `08-WA-OSPF-first-adjacency.png` | First FULL neighbor relationship | [Record](../testing/WA-OSPF-validation.md) |
| `09-WA-OSPF-learned-route.png` | First dynamic route, AD 110 and cost 2 | [Record](../testing/WA-OSPF-validation.md) |
| `10-WA-OSPF-CORE-02-adjacency.png` | CORE-02 FULL adjacency | [Record](../testing/WA-OSPF-validation.md) |
| `11-WA-OSPF-DSW-02-adjacencies.png` | Two FULL neighbors on DSW-02 | [Record](../testing/WA-OSPF-validation.md) |
| `12-WA-OSPF-before-after.png` | Remote subnet ping 0/5 to 5/5 | [Record](../testing/WA-OSPF-validation.md) |
| `13-WA-OSPF-failover.png` | Alternate route cost 3 and 5/5 ping after convergence | [Record](../testing/WA-OSPF-failover-recovery.md) |
| `14-WA-OSPF-recovery.png` | Preferred route cost 2 restored and final ping 5/5 | [Record](../testing/WA-OSPF-failover-recovery.md) |
| `15-WA-2950T-port-inventory.png` | Test model interface inventory, not a deployment change | [Record](../configurations/WA/04-first-access-switch-trunks.md) |
| `16-WA-DSW-01-trunk.png` | First distribution-side trunk | [Record](../configurations/WA/04-first-access-switch-trunks.md) |
| `17-WA-DTP-negotiated-trunk.png` | Dynamic desirable trunk observed before explicit configuration | [Record](../configurations/WA/04-first-access-switch-trunks.md) |
| `18-WA-ASW-01-static-trunks.png` | Both access-side trunks explicitly configured | [Record](../configurations/WA/04-first-access-switch-trunks.md) |
| `19-WA-DSW-02-trunk.png` | Second distribution-side trunk | [Record](../configurations/WA/04-first-access-switch-trunks.md) |
| `20-WA-DSW-02-VLAN-database.png` | All nine planned VLANs active on DSW-02 | [Record](../documentation/WA-vlan-design-and-vtp-checkpoint.md) |
| `21-WA-ASW-01-VTP-baseline.png` | VTP v1 Server, revision 0, five default VLANs; before Step 48 | [Record](../documentation/WA-vlan-design-and-vtp-checkpoint.md) |

The actual `.pkt` file is a separate pending artifact. Do not infer uninterrupted service or measured convergence duration from the recorded ping tests.
