2025-11-24 14:18
Status:
Flashcards:
Source: [[]]
Tags: [[]]


# Class A IP Addresses

## Subnet Size
The bigger the host portion of the network, the more hosts we can have

The global coordination of Internet IPv4 addressing was performed by **IANA (Internet Assigned Number Authority)**

## Class A

- Class A addresses are assigned to networks with very large number of hosts
- The high order (first) bit in a Class A address is always 0
- The default subnet mask is /8
- Valid network addresses range from 1.0.0.0 to 126.0.0.0 /8
- This allows for 126 networks and 16,777,214 hosts per network

### Reserved Class A Addresses

 - 0.0.0.0/8 is reserved and signified 'this network'
 - 0.0.0.1 to 0.0.0.255 are not valid host addresses
 - 127.0.0.0/8 in Class A is reserved as the loopback address for testing the local computer
 - 127.0.0.1 to 127.255.255.255 are not valid addresses

You would use loopback address to ensure that TCP is working

# Class B and C IP Addresses

## Class B 

- Class B are assigned to medium to large sized networks
- The two high order bits in Class B addresses are always set to **1 0**
- The default subnet mask is /16
- Valid network addresses range from 128.0.0.0 to 191.255.0.0 /16. This allows for 16,384 networks and 65,534 hosts per network

## Class C

- Class C addresses are used for small networks
- The three high order bits in Class addresses are always set to **1 1 0**
- The default subnet mask is /24
- Valid network addresses range from 192.0.0.0 to 223.255.255.0/24. This allows for 2,097,152 networks and 254 hosts per network

## Private Addresses

Valid to be assigned to hosts but are not routable on the public internet. They were originally designed for hosts in a closed private network with no internet connectivity

- Class A: 10.0.0.0 to 10.255.255.255
- Class B: 172.16.0.0 to 172.31.255.255
- Class C: 192.168.0.0 to 192.168.255.255
# Class D and E Addresses

## Class D

- Class D addresses are reserved for multicast addresses
- The four high order bits are always set to **1 1 1 0**
- These addresses are not allocated to hosts and there is no default subnet mask
- Valid addresses range from 224.0.0.0 to 239.255.255.255

## Class E

- Class E addresses are 'experimental and reserved for future use'
- The high order bits are 1111
- These addresses are not allocated to hosts and there is no default subnet mask
- Addresses range from 240.0.0.0 to 255.255.255.255. 255.255.255.255 is the broadcast address for 'this network'

### <span style="color:rgb(255, 0, 0)">Reminder</span>

- Multicast is more targeted and will send through router
- Broadcast will send to all host regardless of if the host wanted it and will not send through router
## References
