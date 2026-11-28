# Project 06 — DHCP and DHCP Relay Test Results

The following ping results are transcribed from the submitted Packet Tracer Command Prompt screenshot. The source PC is not identifiable in the capture, so the table records destination-based results only.

## Observed ping results

| Test ID | Destination | Packets sent | Replies received | Loss | Result |
|---|---|---:|---:|---:|---|
| TC-01 | 192.168.10.11 | 4 | 4 | 0% | Successful |
| TC-02 | 192.168.10.13 | 4 | 4 | 0% | Successful |
| TC-03 | 192.168.20.10 | 4 | 3 | 25% | Reachable; first request timed out |
| TC-04 | 192.168.20.11 | 4 | 3 | 25% | Reachable; first request timed out |

The captured output shows successful replies from both 192.168.10.x destinations. The two 192.168.20.x destinations each returned three replies after the first request timed out.

## Interpretation

- Replies from 192.168.20.x indicate that communication to the other subnet is working in this test.
- The first ping can time out while a device learns the destination MAC address through ARP. This is a possible explanation, not proven by this ping screenshot alone.
- Repeat the ping to 192.168.20.10 and 192.168.20.11. If the ARP entry is now cached and the network is stable, the repeat test should ideally show 4/4 replies.
- The screenshot does not show the source PC's IP configuration, so it does not by itself prove which client sent the pings.
- Ping results alone do not prove DHCP lease assignment. Add an `ipconfig` or PC IP Configuration screenshot to document that each client received an address from the intended DHCP pool.

## DHCP assignment tests — pending evidence

| Test ID | Test | Expected result | Actual result |
|---|---|---|---|
| DHCP-01 | PC0–PC5 obtain DHCP configuration | Address in 192.168.10.0/24 | Pending ipconfig evidence |
| DHCP-02 | PC6–PC8 obtain DHCP configuration through relay | Address in 192.168.20.0/24 | Pending ipconfig evidence |

## Additional evidence to add

- `screenshots/dhcp.png` — DHCP configuration screenshot.
- `screenshots/result.png` — submitted Command Prompt ping results.
- DHCP Server Services > DHCP page showing both pools.
- PC IP Configuration or `ipconfig` output for at least one client from each LAN.
- Router `show ip interface brief` output.
- Router running-config showing `ip helper-address 192.168.10.2`.
- Simulation Mode event list showing DHCP Discover, Offer, Request and ACK.

Do not mark DHCP assignment tests as passed until the assigned IP addresses have been verified on the client PCs.
