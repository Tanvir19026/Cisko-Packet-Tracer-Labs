# EtherChannel with LACP

## Objective
Bundle multiple physical Ethernet links into one logical Port-Channel for aggregate capacity, redundancy, and load distribution across traffic flows.

## Lab topology
- 2 Cisco 2960 switches
- 2 PCs
- Two switch-to-switch links: Fa0/1 and Fa0/2
- VLAN 10 named USERS

## LACP configuration
Apply on both switches (adjust PC-facing access port to match your topology):

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

## Verification
```text
show etherchannel summary
show interfaces trunk
show interfaces port-channel 1
```

Expected summary pattern: `Po1(SU) LACP Fa0/1(P) Fa0/2(P)`.

## Test results
- LACP formed Port-Channel 1.
- PC-to-PC ping succeeded.
- After one physical member link was disconnected, ping continued over the remaining member.

**Note:** EtherChannel increases aggregate bandwidth across multiple flows; a single flow is not guaranteed to use the combined bandwidth of all member links.
