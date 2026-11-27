# Project 02: EtherChannel with LACP

A Cisco Packet Tracer lab demonstrating how multiple physical switch links can be bundled into one logical Port-Channel using Link Aggregation Control Protocol (LACP).

## Objectives

- Connect two Cisco switches using multiple Ethernet links.
- Configure LACP to negotiate an EtherChannel.
- Verify that physical interfaces become members of a logical Port-Channel.
- Observe link redundancy when one member link is disconnected.
- Understand aggregate bandwidth and traffic distribution across flows.

## Topology

![EtherChannel LACP topology](screenshots/etherchannel-lacp-topology.png)

Devices used:
- 2 Cisco 2960 switches
- 2 PCs
- 2 switch-to-switch physical links
- Fa0/1 and Fa0/2 used as EtherChannel member interfaces
- VLAN 10 named USERS

The two physical links between the switches are bundled into Port-Channel 1.

## VLAN and LACP Configuration

Apply the matching configuration on both switches. Adjust PC-facing access ports and trunk settings to match the saved topology.

```text
enable
configure terminal
vlan 10
name USERS
exit
interface range fa0/1 - 2
switchport mode trunk
channel-group 1 mode active
exit
interface port-channel 1
switchport mode trunk
end
```

The `active` mode enables LACP negotiation.

## Verification Commands

```text
show etherchannel summary
show interfaces trunk
show interfaces port-channel 1
show running-config
```

Expected summary pattern:

```text
Po1(SU)  LACP  Fa0/1(P) Fa0/2(P)
```

Here, `S` indicates a Layer 2 Port-Channel, `U` indicates it is in use, and `P` indicates member ports are bundled in the Port-Channel.

## Connectivity Tests

The following results were observed during the lab:

| Test ID | Action | Result |
|---|---|---|
| TC-01 | Verify LACP Port-Channel formation | Pass |
| TC-02 | PC-to-PC ping | Pass |
| TC-03 | Disconnect one physical member link and repeat ping | Pass |

Connectivity remained successful after one physical member cable was disconnected, using the remaining member link.

## Key Notes

EtherChannel provides aggregate bandwidth across multiple traffic flows and link redundancy. A single flow is not guaranteed to use the combined bandwidth of all member links.

## Files

- `etherchannel_lacp.pkt` — Packet Tracer lab file.
- `screenshots/etherchannel-lacp-topology.png` — submitted topology screenshot.

## Learning Outcomes

This lab demonstrates LACP negotiation, logical Port-Channel interfaces, EtherChannel member states, link redundancy, and basic EtherChannel verification.
