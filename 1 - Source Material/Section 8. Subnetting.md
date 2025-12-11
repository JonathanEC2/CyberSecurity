
2025-12-02 16:08
Flashcards:
Source: [[]]
Tags: [[]]

# CIDR Classless Inter-Domain Routing

A problem with classful addresses was that if a company had more than 254 hosts, they would need to be assigned a Class B network. They would have much less than 65,534 hosts which would waste a huge amount of global addresses

CIDR removed the fixed /8, /16. /24 requirements for the address classes and allowed them to be split up or 'subnetted' into smaller networks. 

## CIDR and Route Summarization

Another benefit of CIDR is that aggregate blocks of networks can be advertised on the Internet

![[../attachments/Pasted image 20251202161954.png]]

- ISP A does not know about all 255/24 networks reachable on ISP B, it only has a single 175.11.0.0/16 summary route. This reduces the size of ISP A's routing table and takes up less memory
- If an individual link goes down in ISP B, it has no impact on ISP A. 

# Subnetting Overview

## Borrowing Host Bits

In this example, we are a network designer for a small business with four departments spread over two offices and we want to manage our own public address space. Rather than purchasing separate address ranges for different departments, we can purchase a single range and subnet it into smaller portions

Lets say we've been allocated Class C 200.15.10.0/24

- To subnet the network into smaller subnets, we need to 'borrow' host bits and add them to the network portion of the address
- The network address line always moves to the right when we subnet. The further right we go, the more subnets we'll have of that size but less hosts

## Calculating the Number of Networks

 2^subnet-bits
	- If a Class C network uses a /28 subnet mask then we've borrowed 4 bits from the default /24. **2^4 = 16** available subnets
	-
	- If a Class B network uses a /28 subnet mask then we've borrowed 12 bits from the default /16. **2^16 = 4096** available subnets

Hosts on different subnets need to go via router if they want to communicate with each other

## Calculating the Number of Hosts

**2^host-bits - 2**. We subtract 2 because the network address and broadcast address cannot be assigned to hosts
	If a Class C network uses a /28 subnet mask then we have 4 bits left for hosts. **2^4 -2 =14**
	 If a Class B network uses a /28 subnet mask then we have 4 bits left for hosts. **2^4 -2 =14**

## ip subnet-zero

- In the original Internet standards, we used to not allow network bits of all 0's or all 1's. There wasn't really any need for this and it wasted address spaces.
- The `ip subnet-zero` command on a router overrides the limitation, and is enabled by default

# Subnetting Class C Networks and VLSM

## Class C /31 Subnet

Lets say we've been allocated Class C 200.15.10.0/24

Moving all the way too the right would give us /31. This leaves one bit for the host address with a possible value of 0 or 1. It borrows 7 bits from the network address which gives us 128 subnets that accommodate 2 hosts each

We subnet using /31. Valid host addresses:
- 200.15.10.0 to 200.15.10.1
- 200.15.10.2 to 200.15.10.3
- etc up to 200.15.10.254 to 200.15.10.255

/31 breaks the standard rules of IP addressing. /31 subnets are supported on Cisco routers for point-to-point links (we have no need for a network or broadcast address)

## Class C /30

Class C 200.15.10.0/24

Move the line back one space to /30. This leaves 2 bits for the host address. 2^2 -2 = 2 possible hosts. It borrows 6 bits from the network address. This gives us 64 subnets 2^6 which accommodate 2 hosts each

Notice that /30 subnet stop at the 4 bit value, This means the network address will go up in values of 4

Valid host addresses:
- 200.15.10.1 to 200.15.10.2 (network .0, broadcast .3)
- 200.15.10.5 to 200.15.10.6 (network .4, broadcast .7)
- etc up to 200.15.10.253 to 200.15.10.254 (network .252, broadcast .255)

## /31 vs /30

/31 and /31 both accommodate 2 hosts per subnet
/31 supports 128 subnets, /30 only 64
/31 is useful if you need to maximize use of your address space, /30 is more commonly used.
<span style="color:rgb(255, 0, 0)">For CCNA, use /30 to support 2 hosts unless otherwise instructed</span>

## Other Class C Subnet Masks

/29 (255.255.255.248) - 32 subnets, 6 hosts each
/28 (255.255.255.240) - 16 networks, 14 hosts each
/27 (255.255.255.224) - 8 networks, 30 hosts each
/26 (255.255.255.192) - 4 networks, 62 hosts each
/25 (255.255.255.128) - 2 networks, 126 hosts each
/24 (255.255.255.0) - 1 network. 254 hosts each



# Subnetting Practice Question

**What are the network address, broadcast address, and valid host addresses for the IP address 198.22.45.173/26?**

The network portion of the address is the first 26 bits of the address. **192.22.45.128** will be the network address. 
	Another way to calculate network address is  to determine the block size of each subnet and see where the address falls between those blocks. The block sizes of /26 are 64 so the blocks will be 0,64,128,192. 173 falls between 192 and 128 so 128 will be the network address

The broadcast address is the last address in the subnet range which is one less than the next network address. The block size is 64, so the next network address will be 198.22.45.192. Therefore, the broadcast address is **198.22.45.191**

Host address will be everything between network address and broadcast address

*When we subnet a Class C address, all the work is done in the last subnet. The first three octets will remain unchanged*

# Variable Length Subnet Masks

Fixed Subnet Masking required all subnets to be the same size. You couldn't have a subnet with 14 hosts and another with 64 in the same network. All modern routing protocols support Variable Length Subnet Masking. This allows us to size subnets differently according to how many hosts they have.

## Subnetting Considerations

- Locations in network
- Hosts in each location
- IP addressing requirements (should different departments or types oof hosts be in different subnets?)
- Appropriate size for each subnet (don't waste space but leave room for growth)

## Subnetting Design Steps

- Find the largest segments and allocate a suitable subnet size for it
- Allocate this subnet at the start of the address space (largest to smallest)

*In the real world you want a scalable design - you would allocate spare subnets and hosts for future growth. <span style="color:rgb(255, 0, 0)">In the CCNA exam, do exactly as the questions ask, do not worry about best practice</span>


![[../attachments/Pasted image 20251204181131.png]]
In the above example, we are allocated **200.15.10.0/24**

|              | <b><u>Engineering</u></b>                                                        | <b><u>Sales</u></b>                                                              | Router                                                                           |
| ------------ | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- |
| **Subnet**   | 200.15.10.0/27<br>8 Networks<br>30 hosts (32 block size)<br><br>                 | 200.15.10.64/28<br>16 networks<br>14 hosts (16 block size)<br><br>               | 200.15.10.96/30<br>62 Networks<br>2 hosts<br><br>                                |
| **New York** | Net Add - 200.15.10.0<br>Broad Add - 200.15.15.31<br>Hosts - 200.15.10.1 to 30   | Net Add - 200.15.10.64<br>Broad Add - 200.15.10.79<br>Hosts - 200.15.10.65 to 78 | Net Add - 200.15.10.96<br>Broad Add - 200.15.10.99<br>Hosts - 200.15.10.97 to 98 |
| **Boston**   | Net Add - 200.15.10.32<br>Broad Add - 200.15.15.63<br>Hosts - 200.15.10.33 to 62 | Net Add - 200.15.10.80<br>Broad Add - 200.15.10.95<br>Hosts - 200.15.10.81 to 94 | Net Add - 200.15.10.96<br>Broad Add - 200.15.10.99<br>Hosts - 200.15.10.97 to 98 |

Use first available address as the IP address on our routing interfaces

![[../attachments/Pasted image 20251204153725.png]]

# Subnetting Large Networks

## Example 1 - Class B on 4th Octet

In this example, we are allocated Class B **135.15.0.0/16**

IP address 135.15.10.138/29 (255.255.255.248)

- If we subnet this into /29 subnets, we have 3 bits for host addressing. This allows 6 hosts per network (2^3-2)
- Because we were allocated a Class B /16 address range, we have 13 bits for network addresses. This allows for (2^13)

## The Magic Number Method

For the IP address 135.15.10.138/29 (255.255.255.248)

Subtract the value in the subnetted octet from 256: 256-248 = 8. This means the network address goes up in multiples of 8. Find which multiple of 8 is closest to 138. In this case, it would be 136. Add 8 to that to find the next network address

Net address 135.15.10.136
Next Network 135.15.10.144
Broad address 135.15.10.143
Valid host address 135.15.10.137 to 142

## Example 2 - Class A on 4th Octet

In this example, we are allocated Class A **60.0.0.0/8**

## Example 3 - Class A on 3rd Octet

In this example, we are allocated Class A **60.0.0.0/8**




## References


