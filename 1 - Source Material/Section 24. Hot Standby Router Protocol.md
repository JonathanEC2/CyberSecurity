2026-02-12 21:57
Tags: [[]]

# Network Redundancy

- The point of redundancy is to eliminate single points of failure
- We typically do not implement redundancy at the Access Layer because end hosts only have one NIC. Servers with redundant NICs are exception
- In a real world network, the Core/Distribution Layer switches would typically be Layer 3 aware
# First Hop Redundancy Protocol (FHRP)

When you have redundant gateways, configuring half your PC's to use one gateway while the other half uses the other gateway would be inconvenient and would require manual reconfiguration on the PCs to fail over if one of the routers failed

## FHRP

- FHRP uses a Virtual IP (VIP) which is negotiated between gateways. They talk to each other and they agree on what virtual IP address is going to be. There is also an associated virtual MAC address. They negotiate on which router will be answering on which particular IP  and MAC address
- The hosts use the VIP as their default gateway address. If a physical gateway fails, another gateway will take over

### Types of FHRP

- Hot Standby Router Protocol (HSRP): Cisco proprietary. Deployed in active/standby pair
- Virtual Router Redundancy Protocol: Open standard, deployed in active/standby pair very similar to HSRP
- Gateway Load Balancing Protocol: Cisco proprietary, supports active/active load balancing across multiple routers
# Hot Standby Router Protocol

HSRP uses a Virtual IP (VIP) and MAC address to allow for automated failover
The hosts use the VIP as their default gateway address. If a physical gateway fails, another gateway will take over

## HSRP Operations

- Both routers have a unique physical IP and MAC addresses on their interface HSRP interface. They also have the HSRP virtual IP and MAC address configured on their interface. The same address is used on both routers
- When they come online, one is elected the HSRP active router, the other is on standby. The active router owns the virtual IP and MAC address and responds to the ARP requests. All traffic for the VIP go through the active route
- The routers send hello messages to each other over the HSRP interface. If the standby router stops receiving hellos from the active, it will transition to the active router. It will take ownership of the VIP and MAC address and respond to ARP requests
<span style="color:rgb(255, 0, 0)">- Configured on the interface level on the interface facing the hosts</span>


## HSRP Configuration

R1:
```IOS
interface {}
ip address {physical interface}
no shutdown
standby 1 ip {}

```

R2:
```IOS
interface {}
ip address {physical interface}
no shutdown
standby 1 ip {}

```

`sh standby`

Higher IP address will be preferred as active router by default
# HSRP Advanced Topics

## Priority and Pre-emption

- You can choose which router will be the active by setting priority on the routers
- The router with the highest priority will be preferred (default is 100). In the event of a tie the highest IP address wins
- If pre-emption is also enabled, when a higher priority router comes back online after a failure it will transition back to active. If it is not enabled, the lower priority router will remain active when the failed router comes back online. This can be more stable if a higher priority router is flapping

## HSRP Configuration

R1:
```IOS
interface {}
ip address {physical interface}
no shutdown
standby 1 ip {}
standby 1 priority {}
standby 1 preempt
```

R2:
```IOS
interface {}
ip address {physical interface}
no shutdown
standby 1 ip {}
standby 1 priority {}
```

## HSRP Version

- Version 2 introduces a few minor improvements, the default is 1
- Both routers must be running the same version

just add `version 2` when configuring

## Active/Active HSRP Option 1

Within the same group, there will only ever be one router active. To get two active routers,  we can configure two different HSRP groups with different IP addresses

![[attachments/HSRP Two Groups.png]]

## Active/Active HSRP Option 2

If we have multiple subnets going through the same pair of routers, we can have one subnet going through one router and the other subnet going through the other

![[attachments/HSRP Multi Subnet.png]]

You can use the same group number under different interfaces


## References
