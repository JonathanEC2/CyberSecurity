---
sr-due: 2025-10-23
sr-interval: 168
sr-ease: 243
---
[[../2 - Tags/Networking|Networking]]
#network_services 
#review 
## DHCP
When you access a network, the following need to be configured:
- IP address
- Router (Gateway)
- DNS Server

You should manually configure servers as they are not expected to move networks. Also, other devices need to connect to them and find them at a specific address

Automating configuration has many advantages:
- It saves us from having to manually configure the network which is extremely important for mobile devices
- Saves us from address conflicts

<mark style="background: #FFF3A3A6;">DHCP</mark> is an application level protocol that operates on UDP. Port 67 for server listening and 68 for clients sending 

DHCP follows four steps;; Discover, Offer, Request, and Acknowledge (DORA):
<!--SR:!2025-06-29,101,250-->
1. Discover: Client broadcasts a DHCPDISCOVER message seeking the local DHCP server if one exists. Uses 255.255.255.255
2. Offer: Server responds with a DHCPOFFER message with an IP address available for the client to accept
3. Request: Client responds with a DHCPREQUEST message to indicate that it has accepted the offered IP
4. Acknowledge: Server responds with a DHCPPACK message to confirm that the offered IP  address is now assigned to the client

## ARP: Bridging Layer 3 Addressing to Layer 2 Addressing

Whenever one hosts needs to communicate with another host on the same network (ethernet or Wi-Fi), <span style="color:rgb(255, 0, 0)">it must send the IP packet within the data link layer frame</span> .  Although it knows the IP address of the target host, it needs to look up the targets MAC address so the proper data link layer can be created

Devices on the same Ethernet network do not need to know each others MAC addresses all the time; they only need to know it while communicating. Everything else revolves around IP address. 

**ARP** makes it possible to find MAC addresses of another device on the Ethernet. It is encapsulated directly in Ethernet frame

## ICMP: Troubleshooting Networks

**ICMP** is mainly used for network diagnostics and error reporting . Two common commands are:
- <span style="color:rgb(255, 192, 0)">ping</span>: tests connectivity to a target and measures round-trip time (RTT)
- <span style="color:rgb(255, 192, 0)">traceroute</span>: discovers route from your host to a target

### Ping

Sends ICMP Echo Request (Type 8)
Computer on receiving end responds with and  ICMP Echo Reply (Type 0)
<span style="color:rgb(0, 176, 240)">-c 4</span>   tell the ping command to stop after sending four packets

### Traceroute

Makes every router between our system and a target reveal itself

TTL indicates the maximum number of routers a packet can travel through before it is dropped. The router decrements the packets TTL by one before it sends it across. When TTL reaches zero, the router drops the packets and sends an ICMP Time exceeded message (Type 11) <u>(In this context, “time” is measured in the number of routers, not seconds.)</u>

Some routers respond and show their public IP address, and this would let us look up their domain name and discover their geographic location.

## Routing
#routing
- **OSPF (Open Shortest Path First)**;; Allows users to share information about the network topology and calculate the most efficient paths of data transmission. Does so by having routers exchange updates about the state of their connected links and networks
<!--SR:!2025-07-09,104,250-->
- **EIGRP (Enhanced Interior Gateway Routing Protocol)**;; Cisco proprietary routing protocol. Allows routers to share information about the networks they can reach and the cost associated with these routers
<!--SR:!2025-08-14,95,210-->
- **BGP (Border Gateway Protocol)**;; Primary protocol used by the Internet. Allows different networks to exchange routing information and establish paths for data to travel between these networks
<!--SR:!2025-05-18,33,150-->
- **RIP (Routing Information Protocol)**;; Often used in small networks. Shares information about the networks they can reach and the number of hops required to get there.  As a result, each router builds a routing table based on this information, choosing the routes with the fewest hops to reach each destination.
<!--SR:!2025-05-22,53,190-->

## NAT

One public IP address provides Internet access to many private IP addresses.  The router maintains a table that maps the internal IP address and port number with its external IP address and port number. 