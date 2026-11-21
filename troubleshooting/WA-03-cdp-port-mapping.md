# WA-03 — CDP port mapping correction

The original plan assigned CORE-02 Gi0/1 to DSW-01 and Gi0/2 to DSW-02. The actual cabling differed. The command do show cdp neighbors on CORE-02 confirmed Gi0/1 connected to DSW-02 Gi0/1, and Gi0/2 connected to DSW-01 Gi0/2.

Rather than recable, the address assignments on CORE-02 were corrected: Gi0/1 received 10.10.250.13/30 and Gi0/2 received 10.10.250.9/30. The corresponding distribution ports were configured with .14 and .10. Both remote ping tests subsequently returned 5/5.

Lesson: use discovery output to validate actual connections before assigning addresses. Update the as-built port map when wiring differs from design.

## Visual evidence

- [04-WA-CDP-port-discovery](../screenshots/04-WA-CDP-port-discovery.png)
- [06-WA-03-peer-ping](../screenshots/06-WA-03-peer-ping.png)
- [07-WA-04-peer-ping](../screenshots/07-WA-04-peer-ping.png)

[Complete screenshot index](../screenshots/README.md)
