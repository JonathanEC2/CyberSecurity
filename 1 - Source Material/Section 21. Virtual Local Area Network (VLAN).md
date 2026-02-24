2026-02-03 13:20
Tags: [[]]


# Campus LAN Design - Access, Distribution and Core Layers

Campus LAN should be designed for scalability and performance. To aid in best practice design process, the network is split into **access**, **distribution**, and **core** layers

## Access Layer

- This is where your end hosts plug in (desktop computers, servers, IP phones). It is designed to have a high port count at an affordable cost.
- Desktops typically only have one NIC so they connect into one switch or WAP
- Servers often have dual NICs and connect to a pair of redundant switches
- Client access security measures area enabled at this layer

## Distribution Layer

- Access Layer uplinks to this layer
- Switches at this layer serve as an aggregation point for the Access Layer and provide scalability. These switches are typically deployed in redundant pairs with downstream Access Layer switches connected to both
- End hosts are connected here
- Most software policy is enables at this layer

## Core Layer

- Distribution Layer uplinks to this Layer; links all the buildings together. Typically deployed in redundant pairs with downstream Distribution Layers connected to both
- Traffic between different parts of the campus travel through the core so it is designed for speed and resiliency
- Software policy should be avoided at this layer

![[attachments/Tradition Campus Design.png]]


## Collapsed Distribution and Core

Smaller campuses do not need the scalability of three separate layers. In this case, the Distribution and Core Layer functions are performed on the same hardware

# Spine-Leaf Network Design

Traditional campus design is good for traffic that is flowing North and South, meaning traffic is flowing up and down. Traffic would be going up the data center and down to the clients in the other buildings
In modern day data centers, there is a lot more East and West traffic meaning that datacenters are communicating between each other and not just to end clients
All leaf switches are connected to spine switches. This makes scalability easier as you can easily add in addition switches. Performance is also better as each data center is only two hops away

![[attachments/Spine Lead Network Design.png]]

# Why We Have VLANs

## Router Operations

- Routers operate at Layer 3. Host in separate IP subnets must send traffic through a router to communicate. This provides security and performance by splitting networks into smaller domains
- Security rules on routers or firewalls can be used to easily control what traffic is allowed between different IP subnets at Layer 3
- Routers do not forward broadcast traffic by default

## Switch Operations 
- Operate at Layer 2
- Forward traffic by default
- By default, a campus switched network is one large broadcast domain domain 
- **Flood broadcast traffic everywhere including between different IP subnets which raises performance and security concerns**


Unicast Traffic:
![[attachments/Unicast Traffic on Switch.png]]

Broadcast Traffic:
![[attachments/Broadcast Traffic on Switch.png]]

## The Problem

- Switches flood traffic everywhere including between different IP subnets. This affects security because the traffic bypassed router or firewall security policies
- It affects performance because every end host has to process traffic. It also affect performance by using bandwidth on links where traffic is not required

## Virtual Local Area Network

- VLANs segment the LAN into separate broadcast domains at Layer 2
- There is typically a one-to-one relationship between an IP subnet and VLAN
- This improves security and performance


# VLAN Access Ports

- VLAN Access Ports are configured on switch interfaces where end hosts are plugged in
- Access ports are configured with one specific VLAN
- The configuration is only on the switch, the end host is not VLAN aware
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

```IOS
show interface f0/1 switchport
```

# VLAN Trunk Ports

## Dot1Q

An access port carries traffic for one specific VLAN
.1Q trunks are configured on the links between switches where traffic needs to be carried for multiple VLANs

When the switch forwards traffic to another switch, it tags the Layer 2 .1Q header with the correct VLAN. The receiving switch will only forward the traffic out all ports that are in that VLAN. The switch removes the .1Q header from the Ethernet frame when it sends it to the host

## Trunk Port Configuration

SW1:
```IOS
interface {interface}
description {}
switchport trunk encapsulation dot1q
switchport mode trunk

```

Older switches support both ISL and Dot1Q. Older switches require  `switchport trunk encapsulation dot1q` because they'll default to ISL
## Voice VLAN Configuration

VoIP uses the same LAN cable for voice and data. We need to separate voice traffic from data traffic because voice traffic is very sensitive to delay and for security purposes as well. 
The cable running from the switch to the IP phone will be configured as a trunk port which will be carrying voice and data VLAN traffic

```IOS
interface {interface}
description
switchport mode access
switchport access vlan {vlan}
switchport voice vlan {vlan}
```

Even though we specified switchport mode access , it will still act as a trunk port  
## The Native VLAN

- The switch needs to know which VLAN to assign traffic which comes in untagged on a trunk port. The Native VLAN is used for this. 
- The default Native VLAN is VLAN 1. There are security issues with using VLAN 1 as the Native VLAN so best practice is to change it to an unused VLAN
- The Native VLAN must match on both sides of a trunk for it to come up

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

# Dynamic Trunking Protocol (DTP)

If two switches are cabled together they can negotiate a trunk connection using Cisco's Dynamic Trunking Protocol. USING THIS IS NOT RECOMMENDED, manually configure switch ports

## DTP configuration

`switchport mode dynamic auto` will form a trunk if the neighbor switch port is set to trunk or desirable. Trunk will not be formed if both sides are set to auto. Default on newer switches
`switchport mode dynamic desirable` will form a trunk if the neighbor switch port is set to trunk, desirable, or auto. Default on older switches
`switchport nonegotiate` disables DTP

# VLAN Trunking Protocol (VTP)

- Allows you to add, edit, or delete VLANs on switches configures as VTP Servers, and have other switches configured as VTP Clients synchronize their VLAN database with them
- This can be convenient if you manage a large campus
- You will still need to perform port level VLAN configurations on the switches

<span style="color:rgb(255, 0, 0)">Be careful if using VTP - if you accidentally introduce a switch with a higher VLAN database revision number into the domain, it will wipe out all your production VLANs</span>
If using both DTP and VTP, the VTP domain name has to match on neighbor switches for trunks to be formed by DTP

## VTP Modes

- VTP Server: can add, edit, or delete VLANs. A VTP server will synchronize its VLAN database from another server with a higher revision number. Only one server acts as the master
- VTP Client: Cannot add, edit, or delete VLANs. A VTP client will sync its VLAN database from the server with the highest revision number
- VTP Transparent: Does not participate in the VTP domain. Does not advertise or learn VLAN info but will pass it on. Can add, edit, or delete its own local VLAN database

## VTP Configuration

Must manually configure on a transparent mode switch because it does not learn anything from the server

```IOS
vtp domain {name}
vtp mode {server} {client} {transparent}

```
## References

