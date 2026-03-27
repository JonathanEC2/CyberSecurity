2026-03-24 18:53
Tags: [[]]

# Why We Need IPv6

## IPv6 Enhancements

IPv6 was designed to support built in security and host mobility

## Dual Stack

 In dual stack implementation, a network interface can have both an IPv4 and an IPv6 address at the same time. It can communicate using either protocol

# The IPv6 Address Format

128 bit address 
Written as X:X:X:X:X:X:X:X (each portion is called a hextet or a piece)

## Address Shortening

- Leading zeros in each field can be removed
- Successive all zero fields can be shortened to '::'
- Successive all zero fields can be shortened only once in an address to avoid confusion

# IPv6 Global Unicast Addresses

## Global Unicast Address Configuration

- Similar to IPv4 public addresses. They are assigned to an individual host and have global reachability
- They are assigned the range 2000::/3
- Internet authorities assign blocks from the overall 2000::/3 range to organizations. A common assignment for a company is a /48 block (ex. 2001:10:10::/48)


```
ipv6 unicast-routing (enables IPv6 routing first)
int {}
ipv6 add {} / {subnetmask}
no shut
```

## Broadcast, Multicast, and Anycast

- IPv6 does not support support broadcast traffic
- It does however support multicast to all hosts on the local subnet (**ff02::1**) which is functionally equivalent
- The Internet Protocol version 6 (IPv6) prefix FF00::/8 is used for multicast addresses
- Many services which use broadcast to 255.255.255.255 in IPv4 use more specific multicast addresses in IPv6
- Anycast addresses are used to send packets to the closest device that is configured with the nearest anycast address

![[../attachments/Pasted image 20260326214027.png]]

# EUI-64 Address

- A Cisco router can generate full IPv6 addresses for itself when given the interface and /64 network to use
- The host portion of the address is derived from the interfaces MAC address which is guaranteed to be globally unique
- A MAC address is a /48 address compared to the host portion of the IPv6 address. FF:FE is injected in the middle of the /48 MAC address to bring it up to 64 bits. Also, the 7th bit is inverted
- The router will borrow the MAC address from the first Ethernet port for non-ethernet port interfaces such as Serial ports

```
int {}
ipv6 address {}/64 eui-64
no shut
```

![[../attachments/Pasted image 20260326213645.png]]


# Unique Local and Link Local Addresses 

## Unique Local Addresses
- Unicast site-local (USL) addresses are used for Unique Local Addressing (ULA). They are similar to IPv4 RFC 1918 private addresses. They are not publicly reachable
- The are assigned from the range FC00::/7 (The first 7 bits are always 1111110)
- Hosts should be assigned /64 addresses
## Link Local Addresses 

- Link local addresses are valid for communication on that link only. <span style="color:rgb(255, 0, 0)">Will not get routed outside of interface on the other side of the router</span>
- They are assigned from the range FE80::/10 - FEB0::/10
- Hosts should be assigned /64 addresses
- Link local addresses can be used for communication that should not go beyond the local link, like routing protocol hello packets and updates. They are mandatory on IPv6 enabled Cisco routers
- Link Local addresses area automatically generated with EUI-64 addresses on IPv6 enabled Cisco router interfaces. The EUI address can be overridden with manual configuration
- <span style="color:rgb(255, 0, 0)">Link local is mandatory</span>, Global unicast and Unique local addresses are optional

# Stateless Address AutoConfiguration (SLACC)

Hosts can be assigned IPv6 addresses through static addressing, DHCPv6, or SLACC
DHCP servers track their MAC address to IP address to IP assignments so this is 'stateful' addressing

## Stateless Addressing AutoConfiguration (SLACC)

- With SLACC, hosts learn the /64 subnet their interface is on from their local router and then use this info to generate their own IPv6 EUI-64 address. Modern OSs randomize the host portion of the address rather than using standard EUI-64 for privacy reasons
- The router does not track which hosts have which IP address so this is 'stateless' addressing
- As well as telling the host which subnet to generate their IP address on, the router tells the hosts to use itself as their default gateway
- A DHCP server is still required to give out information such as DNS server

## SLACC - Router Advertisements 

- When a global unicast IPv6 address is configured on an interface, the Router Advertisements advertising the network prefix are sent out by default
- These ICMP messages are sent to the 'All Nodes' multicast address form the interface's link-local address
- Hosts can also send a 'Router Solicitation' message to request information

## The Unspecific Address 

:: is the unspecific address or unknown address. ::/0 is a default route equivalent to 0.0.0.0 0.0.0.0 in IPv4

## Neighbor Discovery

- The IPv6 version of ARP and it works in the same way
- Rather than using ARP requests and replies, Neighbor Discovery uses ICMP Neighbor Solicitation and Neighbor Advertisements
- Neighbor Solicitation messages are sent to the Solicited-Node multicast address which reaches all hosts on the subnet

`sh ipv6 neighbors`

# IPv6 Static Routes

- IPv6 routing works the same way as IPv4 routing, but the processes are separate, and there are separate IPv4 and IPv6 routing tables
- The routing tables are built the same way, through static routes or dynamic routing protocols
- 
## IPv6 Routing

Enter `ipv6 unicast-routing` to enable IPv6 routing
You can still configure IPv6 addresses on a router without IPv6 unicast routing enabled and send and receive traffic, but the router will not forward traffic to other networks

## IPv6 Static Routes

Functions the same as IPv4 except you use slash notation on target IP address instead of dotted decimal

- A fully specified static route is an IPv6 static route in which the destination network, outbound interface, and next-hop IPv6 address are all configured directly:
	`ipv6 route 2001:db8:a::/32 fastethernet0/1 2001:db8:b::1`

- A directly attached static route specifies the destination IPv6 network and the outbound interface
	` ipv6 route 2001:db8:a::/32 fastethernet 0/1` command

## IPv6 Summary and Default Route

Default Route:
`ip route ::/0 {next hop}`

# LAB

<span style="color:rgb(255, 0, 0)">when troubleshooting, it is best to work from source to destination</span>
## References
