2025-12-23 22:21
Flashcards:
Source: [[]]
Tags: [[]]

# DNS

- DNS resolves a FQDN such as www.cisco.com to an IP address
- Enterprises will typically have an internal DNS server which can resolve the IP address of internal hosts. Hosts will send their DNS queries to this server. If the internal DNS server cannot resolve said query, it will forward the request out to the public DNS server on the Internet
- UDP port 53 (can fail over to TCP)

## Router DNS Commands

`ip domain-lookup` allows a router to be able to resolve hostnames
`ip name-sever` configures a router or device to use specific DNS servers for resolving hostnames to IP addresses

**DNS Server:**
```IOS
ip domain-lookup
ip name-server 172.23.4.1
ip domain-name flackbox.lab (primary domain name)
ip dns server
ip host LinuxA 172.23.4.2
```

**DNS Client:**
```IOS
ip domain-lookup
ip name-server 172.23.4.1
ip domain-list flackbox.lab (additinal suffixes to search)
```

# ARP Address Resolution Protocol

- Sender needs to know the receivers IP and MAC address to form the packet its going to send. We can point the sender directly to the destination IP address or to the FQDN
- DNS maintains a mapping of FQDNs to IP addresses
- ARP is used to map the IP addresses to MAC addresses

ARP replies are saved in a hosts ARP cache so it doesn't need to send an ARP request every time it wants to communicate

## ARP for Routed Traffic

When the sender and receiver are on different subnets, the traffic must be forwarded by a router 

1. Sender will send ARP request for default gateway IP. Destination MAC for an ARP request is always FFFF.FFFF.FFFF (broadcast address)
2. Router will see its an ARP request for itself and respond to the sender
3. The sender holds the IP packet for the final destination while it sent out the ARP request. It now knows where to send IP packet for the destination MAC address so it will the forward the IP packet ( <span style="color:rgb(255, 0, 0)">IP addresses never change in IP packet, MAC addresses change from physical hop to physical hop</span>)
4. Router does not know receivers MAC address, holds IP packet while it sends an ARP request for the destination IP
5. Receiver responds to ARP request, router now knows its MAC address

`sh arp`

# Life of a Packet

## DNS

1. Host A (10.10.10.10/24) want to send a packet to the FQDN www.flackbox.com but doesn't know the destination IP address. It will hold onto the packet and send a <span style="color:rgb(0, 176, 240)">DNS request</span> to its DNS server at 10.10.100.10
2. Host A compares its IP address and subnet mask to the destination address of the DNS server server, sees its on a different subnet, so the <span style="color:rgb(0, 176, 240)">DNS request</span> needs to be sent via its default gateway
3. Host A will hold the DNS request and send a broadcast ARP request for its default gateway at 10.10.10.1
4. ARP request will be received by switch, Switch 1 will add Host A's MAC address to Port 1.
5. Switch 1 will flood broadcast traffic out all ports apart from the one it was received on
6. ARP request will hit Router A interface (10.10.10.1). Router A will process the ARP request and see it is for itself. It will then send a unicast ARP reply to Host A
7. Router A will add an entry for Host A mapping its IP address to its MAC address
8. Switch 1 will add an entry linking Router A's MAC address to Port 2
9. Host A will add an entry for Router A mapping its IP address to its MAC address. It will use this whenever it needs to send traffic out to another subnet
10. Switch 1 will send the <span style="color:rgb(0, 176, 240)">DNS request</span> only out Port 2

## HTTP

1. Switch 1 will send the packet to Router A which it already had in its MAC address table
2. Router A does not have any interfaces with 10.10.12.0/24 so it knows it needs to route to get there. This route can be either statically configured or learned dynamically through a routing protocol
3. 

## References

