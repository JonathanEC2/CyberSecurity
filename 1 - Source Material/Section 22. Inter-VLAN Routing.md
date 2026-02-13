2026-02-11 11:46
Tags: [[]]

# Routers with Separate Interfaces

## VLAN and IP Subnets in the LAN

- There is typically a one to one relationship between an IP subnet and a VLAN
- Hosts are segregates at Layer 3 by being in different IP subnets and at Layer 2 by being in different  VLANs
- Hosts in different IP subnets need to send traffic via a router to communicate with each other

## Router with Separate Interface

![[attachments/Router with Separate Interface.png]]

R1:
```IOS
interface FastEthernet 0/1
ip address 10.10.10.1 255.255.255.0
interface FastEthernet 0/2
ip address 10.10.10.1 255.255.255.0
ip route 0.0.0.0 0.0.0.0 203.0.113.2
```

SW1:
```IOS
interface FastEthernet 0/1
switchport mode access
switchport access vlan 10

interface FastEthernet 0/2
switchport mode access
switchport access vlan 20

```

## Router with Separate Interfaces Disadvantages

- You need a separate physical interface for every VLAN, you will inevitably run out of interfaces
- Traffic being routed within the campus has to go up and down physical Ethernet cables to the router
# Router on a Stick

Uses a virtual sub-interface on the router which are all on the same physical interface. 

![[attachments/Router on a Stick.png]]

R1
```IOS
interface f0/1
no ip address
no shutdown
FastEthernet 0/0.10
encapsulation dot1q 10
ip address 10.10.10.1 255.255.255.0
FastEthernet 0/1.20
encapsulation dot1q 20
ip address 10.10.20.1 255.255.2550
ip route 0.0.0.0 0.0.0.0 203.0.113.2
```

SW1
```IOS
interface f0/1
switchport trunk encapsulation dot1q
switchport mode trunk
```

## Router on a Stick Consideration

- You don't need a separate physical interface for every VLAN so you are less likely to run out of interfaces
- Traffic being routed in the campus has to go up and down the same physical Ethernet cable on the router causing more contention for bandwidth than when using separate interfaces

# Layer 3 Switch


![[attachments/Layer 3 Switch.png]]

- When you use a Layer 3 switch, it uses a Switched Virtual Interface (SVI). You would configure the interface VLANs that will act as the default gateways
- Its common that connections to an external network will not use an Ethernet port and Layer 3 switches only support Ethernet. Therefore if you need a different type of interface, you will need a separate dedicated router for that

## Inter-VLAN Routing Configuration

SW1
```IOS
ip routing
interface vlan 10
ip address 10.10.10.1 255.255.255.0
interface vlan 20
ip address 10.10.20.1 255.255.255.0
```

## WAN Routing Configuration

SW1
```
interface f0/1
no switchport
ip address 10.10.100.1 255.255.255.0
ip route 0.0.0.0 0.0.0.0 10.10.100.2
```

R1
```IOS
interface f0/1
ip address 10.10.100.2 255.255.255.0
interface f0/2
ip address 203.0.113.1 255.255.255.0
ip route 0.0.0.0 0.0.0.0 203.0.113.2
ip route 10.10.0.0 255.255.0.0 10.10.100.1
```

## Layer 3 Switch Lab

If you've got a fast0/0 and a fast0/1, use 0/0 as the outside, because the 0 looks kind of like an O and use fast 0/1 as the inside because the one looks like an I for inside.
## References


