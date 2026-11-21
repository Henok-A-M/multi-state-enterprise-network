# WA-01 — Distinguishing self-ping from peer connectivity

During verification, both switches initially pinged their own configured IP addresses. These tests returned 5/5 responses, but did not validate Ethernet/IP communication across the link.

Resolution: identify the current device from its IOS hostname and ping the other switch's address. From WA-DSW-01, ping 10.10.250.1. From WA-CORE-01, ping 10.10.250.2.

The user reported the corrected test succeeded. A subsequent screenshot confirmed the correct CORE-01 to DSW-01 peer ping (5/5 replies).

Lesson: a successful command is not necessarily a valid test of the intended requirement. Verify the source, destination and test objective before recording results.

## Visual evidence

- [02-WA-01-peer-ping](../screenshots/02-WA-01-peer-ping.png)

[Complete screenshot index](../screenshots/README.md)
