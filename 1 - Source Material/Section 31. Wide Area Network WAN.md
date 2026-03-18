2026-03-08 21:35
Tags: [[]]

# WAN Overview

- A LAN is a network that connects computers and other devices in a relatively small area, typically a building or group of buildings
- A WAN is a geographically distributed network that connects multiple Local Area Networks together
- A Metropolitan Area Network (MAN) is a network that connects computers and other devices in a geographic area larger than a LAN but smaller than a WAN

# Virtual Private Networks

- A private network uses links which are dedicated for an individual organization
- A Virtual Private Network provides a virtual tunnel between private networks across a shared public network such as the Internet
- Traffic traveling across the tunnel is encrypted and only readable by the authorized used on both sides. Users can share data over the tunnel as if they were connected with a dedicated private link

## Site-to-Site VPN

These connections are terminated on a router or firewall in each office
Software does not need to be installed on users desktop
IPsec is typically used for encryption

### Site-to-Site IPsec VPN Configuration Options

- IPsec Tunnel: open standard IPsec tunnel, does not support multicast
- **General Routing Encapsulation (GRE) over IPsec Tunnel:** adds support for multicast (useful for advertising routing protocols)
- IPsec VTI (Virtual Tunnel Interface): Cisco proprietary simplified configuration, supports multicast
- **Dynamic Multipoint VPN (DMVPN)**: Cisco proprietary. Scalable simple hub and spoke style config enables full mesh connectivity between all offices
- FlexVPN: Newer version of DMVPN
- **Group Encrypted Transport VPN** (GETVPN): Scalable centralized policy for VPN over nonpublic infrastructure (ex. MPLS)

## Remote Access VPN

These connections are between router or firewall in the office and VPN software installed on an individual user's device
The users can access the VPN from anywhere with Internet connectivity
They usually use SSL (Sometimes IPsec) for encryption

# WAN Connectivity Options

Service providers will typically provide an SLA with guarantees for uptime and traffic delay and loss on the link

## Primary WAN Connectivity Options

Leased lines and Satellite can be used for connectivity to the Internet, for direct connectivity between offices, and/or connectivity between offices over VPN
MPLS uses a shared core infrastructure at the service provider. It can be used for connectivity to the Internet and/or connectivity between offices over VPN

## Optical Fiber

Optical fiber is more suitable for long distances than copper wire
It is commonly used for connections between a service providers main locations
FTTX

### SONET and SDH

SONET and SDH are the standards used in service provider optical fiber networks

### Dense Wavelength Division Multiplexing (DWDM)

- Combines multiple optical signals into one optical signal transmitted over a single fiber strand. Each signal is assigned a different wavelength
- Inexpensive scalability
- DWDM is used in all modern long haul optical connections

### Dark Fiber

Unused optical fiber

## Interface Cards

- Routers will typically come with on board Ethernet ports. Additional Ethernet interfaces can be added
- Ethernet is often used for WAN connections today
- Other WAN interfaces are modular and fit into spare slots on the router. Different cards are compatible with different router platforms so be careful when selecting your card

# Leased Lines

- A leased line is a dedicated physical connection between two locations
- It has fixed reserved bandwidth which is not shared with anyone else
- The same bandwidth is available in both directions
- The company may own the cable infrastructure but more commonly it is leased from a service provider for a monthly fee, hence the name

- The first location is typically a corporate office
- The second location is typically:
	Another corporate office
	A data center that's connected to the company's existing WAN
	A data center connected to the Internet

- Leased line that directly connect both areas with one side having Internet access
- Both sites have leased lines that connect to the Internet, configure a VPN tunnel that connects the sites
- Combination of the two without. However we wouldn't want corporate traffic going over an Internet VPN, we want it to go over a direct Leased Line. In this case, we could have an SLA on the direct leased line 


![[attachments/Pasted image 20260308225701.png]]

## Leased Line Benefits and Drawbacks

<b><u>Benefits</b></u>
Reserved bandwidth which is not being shared with anyone else
Service provider will typically provide SLA with guarantees for uptime and traffic delay

<b><u>Drawbacks</b></u>
More Expensive
Longer lead time for installation

## Satellite

Same characteristics of leased line, expensive and low bandwidth
Typically only used if it is the only option

## Calls to Customer over PSTN

Calls inside company will go over leased line 
Calls outside will have to use PSTN

# Multi Protocol Label Switching

- Provides WAN connectivity by a service provide
- Traffic from multiple customers can travel over the providers shared MPLS network so this is a VPN service
- Different levels of SLAs for uptime and delay are offered at different price points
- Ethernet connections are typically used to the customers router
- MPLS VPNs provide full mesh topology by default

## Layer 3 MPLS VPN

![[attachments/Pasted image 20260309191101.png]]

CE: Customer Edge
PE: Provider Edge
P: Provider Core device

- MPLS run across the providers core on the PE and P routers
- The customer CE routers do not run MPLS
- The customer CE routers peer at Layer 3 with the providers PE routers
- Static routes or routing protocol run between the CE and PE
- The PE router looks like another customer router to the customer. The providers core routers are transparent to the customer

## Layer 2 MPLS VPN

The CE devices do not peer with the PE devices. The entire provider network is transparent to the customer
The provider network acts like a giant switch. **The customer sites are in the same IP subnet**
This may be required for clustering an application over the WAN

- **Virtual Private LAN Service (VPLS)**: multipoint L2 VPN
- **Virtual PseudoWire Service (VPWS)**: point to point L2 VPN

# Point to Point Protocol over Ethernet (PPPoE)

## WAN backup and Small office Solutions

- Less expensive options often aimed at home user Internet access can be used as Internet VPN WAN backup options in corporate environments
- Typically no SLA with these solutions
- Can be used as primary WAN connections for smaller offices:
	DSL Digital Subscriber Line
	Cable
	Wireless eg 4G

Commonly used in Digital Subscriber Line (DSL) deployments
PPPoE can be configured on either the DSL modem or the router

# WAN Topology Options

Easy way to answer question about topology is if you just think of point-to-point leased lines between offices.

# Hub and Spoke (Star)

![[attachments/Pasted image 20260309193618.png]]

Advantages: Simple, centralized security policy
Disadvantages: Single point of failure, suboptimal traffic flow

# Redundant Hub and Spoke (Star)

![[attachments/Pasted image 20260309193806.png]]

Advantages: removes single point of failure
Disadvantages: Higher cost, suboptimal traffic flow

## Full Mesh

![[attachments/Pasted image 20260309193949.png]]


Advantages: Optimal traffic flow
Disadvantages: Higher complexity and cost

## Partial Mesh

![[attachments/Pasted image 20260309194130.png]]

## Internet Redundancy Options

![[attachments/Pasted image 20260309194309.png]]
# References
