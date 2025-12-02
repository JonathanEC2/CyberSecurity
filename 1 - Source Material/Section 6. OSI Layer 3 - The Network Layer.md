2025-11-18 18:27
Status:
Flashcards:
Source: [[]]
Tags: [[2 - Tags/OSI|OSI]] [[../2 - Tags/IP Address]]


# The IP Header

- Network layer is responsible for routing packets to their destination and QoS
- IP (Internet Protocol) is a layer 3 protocol. It is a connectionless protocol with no acknowledgements at Layer 3
- ICMP and IPSec also operate at Layer 3

## IP Addressing

- IP addressing partitions the overall network into smaller "subnets". This improves performance and makes troubleshooting easier
- There is no logical separation between networks at Layer 2, its done at Layer 3

## IP Header

![[../attachments/Pasted image 20251118193907.png]]

# Unicast, Broadcast and Multicast Traffic

- Unicast is to a single host. Unicast traffic to multiple hosts would send **separate copies** of the same traffic to each individual host
- Broadcast is to all hosts on the subnet. Routers do not forward broadcast traffic. 
- Multicast is sent to multiple interested hosts. Sends **one copy** to multiple destinations

# Converting from Decimal to Binary

Computers work in binary. Pulses are either off or on so there are only two choices (0 or 1). For each column in a number we have two possible choices, 0 or 1. Every time we add a column to the left, the value is multiplied by 2

# IPv4

An IPv4 address us 32 bits long
It is written as 4 octets in a dotted decimal format (192.168.10.15)


| Platform | Command                                 |
| -------- | --------------------------------------- |
| Windows  | ipconfig                                |
| Linux    | ifconfig, ip stat                       |
| IOS      | show ip interface brief, show interface |

## Static vs Automatic Addressing

IP address is usually set manually on servers, printers, and network devices (routers, printers). On desktop computers, they are normally set through Dynamic Host Configuration Protocol (DHCP)

# Calculating IPv4 Address in Binary

| 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   |
| --- | --- | --- | --- | --- | --- | --- | --- |
To set the boundary between logical networks (subnets), the IP address is combined with a subnet mask
# The Subnet Mask

A host is able to send traffic directly to another host on the same subnet via switches. For a host to send traffic to another host on in a different subnet, it must be forwarded by a router. The host therefor needs to understand if the destination is on the same or different subnet. This is what the subnet mask is used for. 

Subnet mask is also 32 bits long and can be written in dotted decimal or slash notation

## Network and Host Portion

A host address is divided into a network portion and a host portion, the subnet mask defines where that boundary is.

## Subnet 'Masking'

![[../attachments/Pasted image 20251122195144.png]]
- The IP address is compared ('masked') with the subnet mask. 
- A 1 in the subnet mask indicates that bit in the IP address us part of the network address. A 0 indicates it is part of the host address
- Subnet masks are always a contiguous set of 1's

## The Host Portion

- The host portion of the address is available to be allocated to the different hosts on the subnet with two exceptions (broadcast address and network address)
- The host portion of the address specifies the individual host and must be unique to that subnet.
- Hosts don' t have to be numbered sequentially
- You can't have two hosts on with the same IP address

### The Network Address

All 0's in the host portion designate the network address and is not allowed to be allocated to a host

### The Broadcast Address

All 1's in the host portion designate the broadcast address for the subnet. Traffic with this destination address will be sent to all hosts in the subnet

# Slash Notation

10.10.10.15 / 255.0.0.0

- The above example can be written as 10.10.10.15/8
- **The network address is 10.0.0.0/8**
## References
