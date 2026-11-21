# Implementation evidence — Washington

21 relevant screenshots from the actual Packet Tracer session are uploaded to this directory. Full-window captures were cropped to remove the local Windows path from the title bar; CLI and topology evidence were preserved. All 21 PNG files were verified present in the repository. All screenshots are displayed inline in the gallery below. No VTP configuration has been performed.

## Screenshot gallery

### Initial placement, 14 representative switches; not a completed topology

![Initial placement, 14 representative switches; not a completed topology](01-WA-initial-switch-layout.png)

[Record](../architecture/enterprise-design.md) · `01-WA-initial-switch-layout.png`

### First routed peer ping, 5/5

![First routed peer ping, 5/5](02-WA-01-peer-ping.png)

[Record](../testing/WA-01-routed-link.md) · `02-WA-01-peer-ping.png`

### Second peer ping, 5/5 before subsequent address error

![Second peer ping, 5/5 before subsequent address error](03-WA-02-peer-ping.png)

[Record](../testing/WA-core-distribution-validation.md) · `03-WA-02-peer-ping.png`

### Actual CORE-02 port mapping

![Actual CORE-02 port mapping](04-WA-CDP-port-discovery.png)

[Record](../troubleshooting/WA-03-cdp-port-mapping.md) · `04-WA-CDP-port-discovery.png`

### Incorrect Gi0/2 address and failed ping

![Incorrect Gi0/2 address and failed ping](05-WA-wrong-device-IP-incident.png)

[Record](../troubleshooting/WA-02-wrong-device-configuration.md) · `05-WA-wrong-device-IP-incident.png`

### Third routed peer ping, 5/5

![Third routed peer ping, 5/5](06-WA-03-peer-ping.png)

[Record](../testing/WA-core-distribution-validation.md) · `06-WA-03-peer-ping.png`

### Fourth routed peer ping, 5/5

![Fourth routed peer ping, 5/5](07-WA-04-peer-ping.png)

[Record](../testing/WA-core-distribution-validation.md) · `07-WA-04-peer-ping.png`

### First FULL neighbor relationship

![First FULL neighbor relationship](08-WA-OSPF-first-adjacency.png)

[Record](../testing/WA-OSPF-validation.md) · `08-WA-OSPF-first-adjacency.png`

### First dynamic route, AD 110 and cost 2

![First dynamic route, AD 110 and cost 2](09-WA-OSPF-learned-route.png)

[Record](../testing/WA-OSPF-validation.md) · `09-WA-OSPF-learned-route.png`

### CORE-02 FULL adjacency

![CORE-02 FULL adjacency](10-WA-OSPF-CORE-02-adjacency.png)

[Record](../testing/WA-OSPF-validation.md) · `10-WA-OSPF-CORE-02-adjacency.png`

### Two FULL neighbors on DSW-02

![Two FULL neighbors on DSW-02](11-WA-OSPF-DSW-02-adjacencies.png)

[Record](../testing/WA-OSPF-validation.md) · `11-WA-OSPF-DSW-02-adjacencies.png`

### Remote subnet ping 0/5 to 5/5

![Remote subnet ping 0/5 to 5/5](12-WA-OSPF-before-after.png)

[Record](../testing/WA-OSPF-validation.md) · `12-WA-OSPF-before-after.png`

### Alternate route cost 3 and 5/5 ping after convergence

![Alternate route cost 3 and 5/5 ping after convergence](13-WA-OSPF-failover.png)

[Record](../testing/WA-OSPF-failover-recovery.md) · `13-WA-OSPF-failover.png`

### Preferred route cost 2 restored and final ping 5/5

![Preferred route cost 2 restored and final ping 5/5](14-WA-OSPF-recovery.png)

[Record](../testing/WA-OSPF-failover-recovery.md) · `14-WA-OSPF-recovery.png`

### Test model interface inventory, not a deployment change

![Test model interface inventory, not a deployment change](15-WA-2950T-port-inventory.png)

[Record](../configurations/WA/04-first-access-switch-trunks.md) · `15-WA-2950T-port-inventory.png`

### First distribution-side trunk

![First distribution-side trunk](16-WA-DSW-01-trunk.png)

[Record](../configurations/WA/04-first-access-switch-trunks.md) · `16-WA-DSW-01-trunk.png`

### Dynamic desirable trunk observed before explicit configuration

![Dynamic desirable trunk observed before explicit configuration](17-WA-DTP-negotiated-trunk.png)

[Record](../configurations/WA/04-first-access-switch-trunks.md) · `17-WA-DTP-negotiated-trunk.png`

### Both access-side trunks explicitly configured

![Both access-side trunks explicitly configured](18-WA-ASW-01-static-trunks.png)

[Record](../configurations/WA/04-first-access-switch-trunks.md) · `18-WA-ASW-01-static-trunks.png`

### Second distribution-side trunk

![Second distribution-side trunk](19-WA-DSW-02-trunk.png)

[Record](../configurations/WA/04-first-access-switch-trunks.md) · `19-WA-DSW-02-trunk.png`

### All nine planned VLANs active on DSW-02

![All nine planned VLANs active on DSW-02](20-WA-DSW-02-VLAN-database.png)

[Record](../documentation/WA-vlan-design-and-vtp-checkpoint.md) · `20-WA-DSW-02-VLAN-database.png`

### VTP v1 Server, revision 0, five default VLANs; before Step 48

![VTP v1 Server, revision 0, five default VLANs; before Step 48](21-WA-ASW-01-VTP-baseline.png)

[Record](../documentation/WA-vlan-design-and-vtp-checkpoint.md) · `21-WA-ASW-01-VTP-baseline.png`

The actual `.pkt` file is a separate pending artifact. Do not infer uninterrupted service or measured convergence duration from the recorded ping tests.
