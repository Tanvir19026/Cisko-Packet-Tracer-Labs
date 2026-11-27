# STP & RSTP Redundant Switching Network

## Objective
Use a three-switch triangle topology to demonstrate Layer 2 loop prevention, root bridge election, port roles, redundant paths, and link-failure recovery.

## Devices
- 3 Cisco 2960 switches: SW1, SW2, SW3
- 3 PCs: PC0, PC1, PC2
- Triangle inter-switch connections

## PC addressing

| PC | IP address | Subnet mask |
|---|---|---|
| PC0 | 192.168.10.10 | 255.255.255.0 |
| PC2 | 192.168.10.20 | 255.255.255.0 |
| PC1 | 192.168.10.30 | 255.255.255.0 |

## Verification commands
```text
show spanning-tree
show spanning-tree summary
show interfaces status
```

## Observations

### Default STP
- SW2 was initially elected Root Bridge.
- Root Bridge MAC: `0001.6301.337D`.
- SW1 Fa0/1 was Root / Forwarding.
- SW1 Fa0/2 was Alternate / Blocking.
- SW3 Fa0/1 was Root / Forwarding.

With equal STP priorities, the lowest Bridge ID won.

### Root bridge change
SW1 was configured with a lower priority and became Root Bridge. Port roles and the redundant blocked path changed after the election.

### Link failure and recovery
The active SW1–SW2 link was disconnected. SW2 selected Fa0/2 as its Root Port through SW3.
- SW1 remained Root Bridge (MAC `0060.4799.E9E2`).
- SW2 root path cost was 38 (two FastEthernet links, cost 19 each).
- PC-to-PC ping succeeded after STP reconvergence.

### RSTP / Rapid-PVST
Configured on all three switches:
```text
enable
configure terminal
spanning-tree mode rapid-pvst
end
show spanning-tree
show spanning-tree summary
```
Verified output included `Switch is in rapid-pvst mode` and `Spanning tree enabled protocol rstp`.

**Evidence note:** The topology screenshot is included. The final measured RSTP failover timing was not recorded, so no numerical convergence-time claim is made.

## Key concepts
- Root Bridge: switch with the lowest Bridge ID.
- Root Port: best path from a non-root switch toward the Root Bridge.
- Designated Port: forwarding port selected for a Layer 2 segment.
- Alternate Port: alternate path toward the Root Bridge, normally non-forwarding while the primary path is available.
- STP/RSTP prevent Layer 2 loops while retaining redundant paths for recovery.
