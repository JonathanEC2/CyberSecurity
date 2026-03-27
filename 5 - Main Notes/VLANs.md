2026-03-20 18:35
Tags: [[]]

# Campus LAN Design - Access, Distribution and Core Layers

Campus LAN should be designed for scalability and performance. To aid in best practice design process, the network is split into **access**, **distribution**, and **core** layers. Best for North and South traffic

## Access Layer

- This is where your end hosts plug in (desktop computers, servers, IP phones). It is designed to have a high port count at an affordable cost.
- Client access security measures are enabled at this layer

## Distribution Layer

Aggregation point for the Access Layer 
These switches are deployed in redundant pairs with downstream access Layer switches
Software policy is enabled here 

## Core Layer

- Distribution Layer uplinks to this Layer; links all the buildings together. Typically deployed in redundant pairs with downstream Distribution Layers connected to both
- Traffic between different parts of the campus travel through the core so it is designed for speed and resiliency
## Collapsed Distribution and Core

Smaller campuses do not need the scalability of three separate layers. In this case, the Distribution and Core Layer functions are performed on the same hardware

# Spine-Leaf Network Design

Good for East and West Traffic which means data centers are communicating between each other and not just clients
All leaf switches connect to spine switches. Leaves never connect to leaves

![[../attachments/Pasted image 20260326183904.png]]

# Why We Have VLANs

- Switches operate at Layer 2 and forward traffic by default. This means by default a campus would be one large broadcast domain
- Flooding traffic everywhere is a huge security and performance concern
-  This affects security because the traffic bypassed router or firewall security policies
- It affects performance because every end host has to process traffic. It also affect performance by using bandwidth on links where traffic is not required

# VLAN Access Ports

- VLAN Access Ports are configured on switch interfaces where end hosts are plugged in
- <span style="color:rgb(255, 0, 0)">Access ports are configured with one specific VLAN</span>
- Switches only allow traffic in the same VLAN

## Access Port Configuration

```IOS
vlan {number}
name {name}
```

```IOS
interface {interface}
switchport mode access
switchport access vlan {number}

interface range FastEthernet 0/3-5
switchport access vlan 10
```

# VLAN Trunk Ports

Dot1Q trunks are configured on the links between switches where traffic needs to be carried for multiple VLANs
When the switch forwards traffic to another switch, it tags the Layer 2 .1Q header with the correct VLAN. The receiving switch will only forward the traffic out all ports that are in that VLAN. The switch removes the .1Q header from the Ethernet frame when it sends it to the host

## Trunk Port Configuration

SW1:
```IOS
interface {interface}
description {}
switchport trunk encapsulation dot1q
switchport mode trunk
```

## Voice VLAN Configuration

- VoIP uses the same LAN cable for voice and data. We need to separate voice traffic from data traffic because voice traffic is very sensitive to delay and for security purposes as well. 
- The cable running from the switch to the IP phone will be configured as a trunk port which will be carrying voice and data VLAN traffic.
- <span style="color:rgb(255, 0, 0)">The voice VLAN is disabled by default, and 802.1x authentication is supported on a voice VLAN</span>
- <span style="color:rgb(255, 0, 0)">When a voice virtual local area network (VLAN) is configured, PortFast is automatically enabled; however, PortFast is not automatically disabled when that same voice VLAN is disabled.</span>


```IOS
interface {interface}
description
switchport mode access
switchport access vlan {vlan}
switchport voice vlan {vlan}
```

## The Native VLAN

- The switch needs to know which VLAN to assign traffic which comes in untagged on a trunk port. The Native VLAN is used for this. 
- The default Native VLAN is VLAN 1. There are security issues with using VLAN 1 as the Native VLAN so best practice is to change it to an unused VLAN
- The Native VLAN must match on both sides of a trunk for it to come up
- <span style="color:rgb(255, 0, 0)">Traffic that is sent untagged over the native VLAN will still be forwarded even if native VLANs do not match. Even though traffic will be forwarded, a VLAN mismatch could cause the traffic to be misdirected or dropped</span>

```IOS
vlan 199
name Native

interface {interface}
description
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk native vlan 199
```

## Allowed VLANs Configuration

We don't want to send traffic to where its not required. No need to send VLAN traffic if there are no devices to send traffic to over the connection

```IOS
interface {interface}
switchport trunk allowed vlan 10,30
```

# Dynamic Trunking Protocol

## DTP configuration

`switchport mode dynamic auto` will form a trunk if the neighbor switch port is set to trunk or desirable. Trunk will not be formed if both sides are set to auto. Default on newer switches
`switchport mode dynamic desirable` will form a trunk if the neighbor switch port is set to trunk, desirable, or auto. Default on older switches
`switchport nonegotiate` disables DTP

# VLAN Trunking Protocol (VTP)

- Allows you to add, edit, or delete VLANs on switches configures as VTP Servers, and have other switches configured as VTP Clients synchronize their VLAN database with them
- You will still need to perform port level VLAN configurations on the switches

## VTP Modes

- VTP Server: can add, edit, or delete VLANs. A VTP server will synchronize its VLAN database from another server with a higher revision number. Only one server acts as the master
- VTP Client: Cannot add, edit, or delete VLANs. A VTP client will sync its VLAN database from the server with the highest revision number
- VTP Transparent: Does not participate in the VTP domain. Does not advertise or learn VLAN info but will pass it on. Can add, edit, or delete its own local VLAN database

## VTP Configuration

Must manually configure on a transparent mode switch because it does not learn anything from the server

```IOS
vtp domain {name}
vtp password {}
vtp mode {server} {client} {transparent}

```

# Inter-VLAN Routing

 Hosts in different IP subnets need to send traffic via a router to communicate with each other

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

## Router on a Stick

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

## Layer 3 Switch

![[../attachments/Pasted image 20260326202713.png]]

Layer 3 Switch uses a Switched Virtual Interface (SVI). You would configure the interface VLANs that will act as the default gateway
Its common that connections to an external network will not use an Ethernet port and Layer 3 switches only support Ethernet. Therefore if you need a different type of interface, you will need a separate dedicated router for that

### Inter-VLAN Routing Configuration

SW1
```IOS
ip routing
interface vlan 10
ip address 10.10.10.1 255.255.255.0
interface vlan 20
ip address 10.10.20.1 255.255.255.0
```

### WAN Routing Configuration

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

# Summary
## References
