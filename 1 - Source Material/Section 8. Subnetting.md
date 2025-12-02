
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

Hosts on different subnets need to goo via router if they want to communicate with each other

## Calculating the Number of Hosts

**2^host-bits - 2**. We subtract 2 because the network address and broadcast address cannot be assigned to hosts
	If a Class C network uses a /28 subnet mask then we have 4 bits left for hosts. **2^4 -2 =14**
	 If a Class B network uses a /28 subnet mask then we have 4 bits left for hosts. **2^4 -2 =14**

## ip subnet-zero

- In the original Internet standards, we used to not allow network bits of all 0's or all 1's. There wasn't really any need for this and it wasted address spaces.
- The `ip subnet-zero` command on a router overrides the limitation, and is enabled by default

## References
