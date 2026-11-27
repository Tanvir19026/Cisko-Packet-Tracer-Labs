# Switch Port Security

## Objective
Restrict the MAC addresses allowed on an access port and demonstrate sticky MAC learning, violation detection, and port recovery.

## Packet Tracer activity
- `port_security.pkt`

## Example configuration
```text
enable
configure terminal
interface fa0/1
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown
end
```

## Verification
```text
show port-security
show port-security interface fa0/1
show port-security address
show mac address-table
show interfaces status
```

## Observed test
- The authorized PC's MAC address was learned as a sticky secure address.
- Replacing the authorized PC with a different PC triggered a port-security violation.
- The port entered Secure-shutdown / err-disabled state.
- After reconnecting the authorized PC and manually recovering the interface, the port returned to Secure-up.

## Recovery
Remove the unauthorized device first, then:
```text
configure terminal
interface fa0/1
shutdown
no shutdown
end
```
