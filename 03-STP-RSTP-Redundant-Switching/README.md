# Project 03: STP and RSTP Redundant Switching Network

A Cisco Packet Tracer lab demonstrating Layer 2 loop prevention, Root Bridge election, spanning-tree port roles, redundant paths, and link-failure recovery using a three-switch triangle topology.

## Objectives

- Build a redundant Layer 2 topology with three switches.
- Observe how STP elects a Root Bridge.
- Identify Root, Designated, and Alternate port roles.
- Observe a redundant port entering the Blocking state.
- Change the Root Bridge by adjusting switch priority.
- Disconnect an active link and observe path recalculation.
- Enable Rapid-PVST and verify the spanning-tree mode.

## Topology

![STP and RSTP topology](screenshots/stp-rstp-topology.png)

Devices used:
- 3 Cisco 2960 switches: SW1, SW2, SW3
- 3 PCs: PC0, PC1, PC2
- Triangle-shaped inter-switch connections

The PCs are connected to the switches and use the same IPv4 subnet.

## IPv4 Addressing Plan

Subnet mask: `255.255.255.0` (`/24`).

| Device | Planned IPv4 address | Subnet mask |
|---|---|---|
| PC0 | `192.168.10.10` | `255.255.255.0` |
| PC2 | `192.168.10.20` | `255.255.255.0` |
| PC1 | `192.168.10.30` | `255.255.255.0` |

## Verification Commands

```text
show spanning-tree
show spanning-tree summary
show spanning-tree root
show interfaces status
```

## STP Observations

### Initial Root Bridge Election

- SW2 was initially elected Root Bridge.
- Root Bridge MAC address: `0001.6301.337D`.
- On SW1, Fa0/1 was Root / Forwarding.
- On SW1, Fa0/2 was Alternate / Blocking.
- On SW3, Fa0/1 was Root / Forwarding.

With equal STP priorities, the switch with the lowest Bridge ID became the Root Bridge.

### Root Bridge Change

SW1 was configured with a lower bridge priority and became the Root Bridge. The port roles and redundant blocked path changed after the new election.

### Link Failure and Recovery

The active SW1–SW2 link was disconnected. SW2 selected Fa0/2 as its Root Port through SW3.

- SW1 remained Root Bridge (MAC `0060.4799.E9E2`).
- SW2 root path cost was 38 (two FastEthernet links, cost 19 each).
- PC-to-PC ping succeeded after STP reconvergence.

## RSTP / Rapid-PVST Configuration

Rapid-PVST was enabled on all three switches:

```text
enable
configure terminal
spanning-tree mode rapid-pvst
end
show spanning-tree
show spanning-tree summary
```

The output confirmed `Switch is in rapid-pvst mode` and `Spanning tree enabled protocol rstp`.

**Evidence note:** The final measured RSTP failover timing was not recorded, so this project does not claim a numerical RSTP convergence time.

## Key Concepts

- Root Bridge: switch with the lowest Bridge ID.
- Root Port: best path from a non-root switch toward the Root Bridge.
- Designated Port: forwarding port selected for a Layer 2 segment.
- Alternate Port: alternate path toward the Root Bridge, normally non-forwarding while the primary path is available.
- STP/RSTP prevent Layer 2 loops while retaining redundant paths for recovery.

## Files

- `stp_rstp.pkt` — Packet Tracer lab file.
- `screenshots/stp-rstp-topology.png` — submitted topology screenshot.

## Learning Outcomes

This lab demonstrates the purpose of STP/RSTP, Root Bridge election, spanning-tree port roles, redundant path blocking, link-failure recovery, and Rapid-PVST verification.
