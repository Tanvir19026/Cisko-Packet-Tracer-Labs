# Project 06 — DHCP and DHCP Relay Test Results

Record the actual Packet Tracer results below after configuring the router and Server-PT.

| Test ID | Test | Expected result | Actual result |
|---|---|---|---|
| TC-01 | PC0–PC5 obtain DHCP configuration | Address in 192.168.10.0/24 | Pending |
| TC-02 | PC6–PC8 obtain DHCP configuration | Address in 192.168.20.0/24 | Pending |
| TC-03 | LAN 1 client pings 192.168.10.1 | Reply received | Pending |
| TC-04 | LAN 2 client pings 192.168.20.1 | Reply received | Pending |
| TC-05 | LAN 2 client pings DHCP Server 192.168.10.2 | Reply received | Pending |
| TC-06 | LAN 1 client pings LAN 2 client | Reply received | Pending |
| TC-07 | LAN 2 client pings LAN 1 client | Reply received | Pending |

## Evidence to add

- DHCP Server Services > DHCP page showing both pools.
- PC IP Configuration or ipconfig output for at least one client from each LAN.
- Router show ip interface brief output.
- Router running-config showing ip helper-address 192.168.10.2.
- Simulation Mode event list showing DHCP Discover, Offer, Request and ACK.

Do not change Pending to Pass until the test has been performed and verified.
