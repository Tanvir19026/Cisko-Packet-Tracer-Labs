# PortFast & BPDU Guard

## Objective
Protect an edge/access port intended for an end device from an unexpected switch connection.

## Configuration
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

## Verification
```text
show running-config
show spanning-tree interface fa0/1 detail
show interfaces status
```

The running configuration confirmed access mode, PortFast, and BPDU Guard.

## Test result
After replacing the PC with another switch on the protected edge port, BPDU Guard detected BPDUs and placed Fa0/1 into an err-disabled state.

## Recovery
Disconnect the unexpected switch first:
```text
enable
configure terminal
interface fa0/1
shutdown
no shutdown
end
```

Use PortFast and BPDU Guard on end-device-facing edge ports, not ordinary switch-to-switch links.
