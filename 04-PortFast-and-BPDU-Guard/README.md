# Project 04: PortFast and BPDU Guard

A Cisco Packet Tracer lab demonstrating edge-port configuration and Layer 2 protection against unexpected switch connections on an end-device-facing access port.

## Objectives

- Configure an access port for an end device.
- Enable PortFast to allow an edge port to transition quickly to forwarding.
- Enable BPDU Guard to protect the edge port.
- Observe the effect of receiving a BPDU on the protected port.
- Verify the err-disabled state and practice interface recovery.

## Topology

![PortFast and BPDU Guard topology](screenshots/bpdu-guard-test.png)

Devices visible in the submitted topology:
- 2 Cisco 2960 switches
- 1 PC
- A protected edge port connecting the test device

The PC-facing switch port is configured as an edge port. During the test, the PC was replaced with another switch to generate BPDUs on that protected port.

## PortFast and BPDU Guard Configuration

On the end-device-facing switch port (example Fa0/1):

```text
enable
configure terminal
interface fa0/1
switchport mode access
spanning-tree portfast
spanning-tree bpduguard enable
end
```

PortFast allows an edge port to move quickly to forwarding. BPDU Guard places the protected port into an err-disabled state when it receives a BPDU.

## Verification Commands

```text
show running-config
show spanning-tree interface fa0/1 detail
show interfaces status
```

The running configuration confirmed access mode, PortFast, and BPDU Guard.

## Test Results

| Test ID | Action | Result |
|---|---|---|
| TC-01 | Verify PortFast and BPDU Guard configuration | Pass |
| TC-02 | Replace the PC with another switch on the protected edge port | BPDU detected |
| TC-03 | Observe protected port state | Err-disabled |

BPDU Guard detected BPDUs from the unexpected switch and placed Fa0/1 into an err-disabled state.

## Recovery

Disconnect the unexpected switch first. Then recover the interface:

```text
enable
configure terminal
interface fa0/1
shutdown
no shutdown
end
```

Use PortFast and BPDU Guard on end-device-facing edge ports, not ordinary switch-to-switch links.

## Files

- `vpduguard_portfast.pkt` — Packet Tracer lab file.
- `screenshots/bpdu-guard-test.png` — submitted topology screenshot.

## Learning Outcomes

This lab demonstrates edge-port configuration, PortFast, BPDU Guard, BPDU detection, err-disabled port protection, and manual interface recovery.
