2026-03-26 20:29
Tags: [[]]

## FHRP

- FHRP uses a Virtual IP (VIP) which is negotiated between gateways. They talk to each other and they agree on what virtual IP address is going to be. There is also an associated virtual MAC address. They negotiate on which router will be answering on which particular IP  and MAC address
- The hosts use the VIP as their default gateway address. If a physical gateway fails, another gateway will take over

### Types of FHRP

- **Hot Standby Router Protocol (HSRP)**: Cisco proprietary. Deployed in active/standby pair
- **Virtual Router Redundancy Protocol (VRRP)**: Open standard, Internet Engineering Task Force (IETF) standard that can use object tracking and preemption to provide Layer 3 failover. Has one master router and multiple backup routers
- **Gateway Load Balancing Protocol**: Cisco proprietary, supports active/active load balancing across multiple routers; Elects an Active Virtual Gateway (AVG) with multiple Active Virtual Forwarders (AVFs)

## HSRP Operations

- Both routers have a unique physical IP and MAC addresses on their interface HSRP interface. They also have the HSRP virtual IP and MAC address configured on their interface. The same address is used on both routers
- When the routers come online, one is active and one is standby. The active router owns the Virtual IP and MAC address
- If standby router stops receiving hellos from the active router, it will transition to the active router and take ownership of the VIP and MAC
- <span style="color:rgb(255, 0, 0)">Configured on the interface level on the interface facing the hosts</span>


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

## Priority and Pre-emption

The router with the highest priority is preferred with a default value of 100. In the event of a tie, the highest IP address wins
If preemption is enabled, when a higher priority router comes back online after a failure, it will transition back to being active

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
## References
