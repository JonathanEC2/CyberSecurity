2026-24-02 18:21
Tags: [[]]

# Why we have EtherChannel

## Campus Design Oversubscription

- A starting rule of thumb recommendation for oversubscription is 20:1 from the Access Layer to the Distribution Layer. Meaning if you had 20 PCs connected with 1 Gbps NIC at the Access Layer, you would require a single 1 Gbps uplink to the Distribution Layer
- The recommendation is 4:1 for the Distribution to Core Layers
- Theses are general values, you should analyze the traffic on your network to verify links are not congested

Switches often have dedicated uplink ports with higher bandwidth than their access ports. For example, a 48 port 1 Gbps switch with a pair of 10 Gbps uplinks. This can help with the subscription ratio

- 48 x 1 Gbps clients = 48 Gbps
- 2 x 10 Gbps = 20 Gbps
- Subscription Ratio = 2.4:1

## Spanning Tree Load Balancing

If we have 2 uplink ports, Spanning Tree will block one. That is because Spanning Tree instances support redundancy but not load balancing. If a switch has multiple equal cost paths to the Root Bridge, it will chose the port with the lowest port ID (such as F0/1). That means we would only be getting half of our bandwidth

## EtherChannel (Port Channel)
LAG Link Aggregation
Link bundle

- EtherChannel groups multiple physical interfaces into a single logical interface
- Spanning Tree sees the EtherChannel as a single interface so it does not block any ports, giving us all of our available bandwidth
- Traffic is load balanced across all links in the EtherChannel
- If an interface goes down its traffic will fail over to the remaining links

## NIC Teaming (Bonding)
Link Aggregation

Combines multiple physical network cards into a single logical interface

# EtherChannel Load Balancing

- A flow is a communication from a client to a server
- A single flow is load balanced onto a single port channel interface. For example, all packets in the flow from PC-1 to Server-1 always go over interface G0/1, all packets in the flow from PC-2 to Server-2 always go over interface G0/2
- Packets from the same flow are not load balanced round robin across all the interfaces in the port channel. This could cause packets to arrive out of order
- Any single flow gets the maximum bandwidth of a single link in the port channel as a maximum. A switch with 4 flows  of 1 Gbps would be an aggregate of 4 Gbps available across all flows

# EtherChannel Protocols and Configurations 


**Link Aggregation Control Protocol (LACP)**
	- Open Standard
	- Switches on both sides negotiate the port channel creation and maintenance 
	- Preferred method

**Port Aggregation Protocol (PAgP)**
	- Cisco Proprietary
	- Switches on both sides negotiate the port channel creation and maintenance 

**Static**
	- Switches do not negotiate creation and maintenance but settings must still match on both sides for the port channel to come up
	- Use if LACP is not supported on both sides

All protocols are configured using the `channel-group` command

## EtherChannel Parameters

Settings that must match:
- Speed and Duplex
- Access or Trunk
- Native VLAN and allowed VLANs on trunks
- Access VLAN on access ports

## LACP Configuration 

LACP interfaces can be set as either **Active** or **Passive**:
- Both Passive - port channel will not come up
- Both Active - port channel will come up
- One Active One Passive - port channel will come up

It is recommended to set both sides as Active so you don't have to think about which side is which

**Configure matching settings on both sides of the link**

This creates the port channel:
```IOS
interface range {}
channel-group 1 mode active
```

This configures the interface settings on the port channel:
```IOS
interface port-channel 1
switchport mode trunk
```


## PAgP Configuration

PAgP interfaces can be set as either **Desirable** or **Auto**:
- Both Auto - port channel will not come up
- Both Desirable - port channel will come up
- One Desirable One Auto - port channel will come up

This creates the port channel:
```IOS
interface range {}
channel-group 1 mode desirable
```

This configures the interface settings on the port channel:
```IOS
interface port-channel 1
switchport mode trunk
```

## Static Configuration

This creates the port channel:
```IOS
interface range {}
channel-group 1 mode on
```

This configures the interface settings on the port channel:
```IOS
interface port-channel 1
switchport mode trunk
```

## Verification - `show etherchannel summary`

`show etherchannel summary`

# Stackwise, VSS, vPC

- Matching EtherChannel settings have to be configured on the switches on both sides of the link
- You can configure separate port channels from a switch to redundant upstream switches
- Spanning tree will see the port channel as two separate interfaces and block one path if a loop is formed

![[../attachments/Pasted image 20260228220219.png]]

## Multi-chassis EtherChannel

- Cisco supports mult-chassis EtherChannel technologies on some switches. These switches support a shared EtherChannel from different switches
- These switches must be configured with matching settings
- Spanning Tree is still enabled but it does not detect any loops
- This supports full load balancing and redundancy across all interfaces3

![[../attachments/Pasted image 20260228220237.png]]

## Stackwise, VSS, vPC

- Multi-chassis EtherChannel is supported on these technologies
- Stackwise on select Catalyst platforms such as the Catalyst 3750, 3850, 9000. When you  configure a StackWise stack, the separate physical switches all operate as if they are one switch and they are configured as if they're one switch as well
- Virtual Switching System (VSS) on select Catalyst Systems such as 4500, 6500. Functions similar to Stackwise
- Virtual Port Channel (vPC) on the Nexus family. Configured as two separate switches with matching configuration

# Layer 3 EtherChannel

```IOS
interface range {}
no switchport
channel-group 1 mode | active | auto | desirable | on | passive

interface port-channel {}
ip address {}
no shutdown

```


Spanning Tree is a necessary evil, it prevents loops but also shuts down half of our links
The benefit you get from using Layer 3 switches everywhere is that it negates the need for spanning tree
In an environment where you have all Layer 3 switches, the default gateway will be on the Access Layer switches

## References