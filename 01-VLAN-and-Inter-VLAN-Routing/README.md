# VLAN & Inter-VLAN Routing Labs

This folder groups the VLAN and Layer 3 gateway labs into one learning track.

## Included Packet Tracer activities

| File | Focus |
|---|---|
| `vlan_inter_vlan_routing.pkt` | VLAN and inter-VLAN routing |
| `vlan_svi.pkt` | Inter-VLAN routing using Layer 3 switch SVIs |
| `vlan_troubleshoting.pkt` | VLAN troubleshooting practice |
| `vlsip.pkt` | VLSM addressing lab |
| `Lab-03-Inter-LAN-Routing.pkt` | Routing between multiple LANs |

## Core topics
- VLAN creation and management
- Access and trunk ports
- IEEE 802.1Q trunking
- Inter-VLAN routing
- Router-on-a-Stick
- Layer 3 switch and SVI
- VLAN troubleshooting
- IPv4 subnetting and VLSM

## Useful verification commands
```text
show vlan brief
show interfaces trunk
show interfaces switchport
show ip interface brief
show ip route
show spanning-tree
```

Open each `.pkt` file in Cisco Packet Tracer and verify the topology and addressing before running tests. The exact port assignments and IP details may vary by activity.
