2026-01-11 18:13
Tags: [[]]

# Dynamic Routing Protocols vs Static Routes

Routers automatically advertise their best path to known networks to each other. Routers use this info to determine their own best path to the known destinations. When the state of the network changes, such as a link going down or a subnet being added, the routers update each other. Routers will automatically calculate a new best path and update the routing table if the network changes

Routers will send updates to adjacent routers (each of the directly connected neighboring routers)

## Summary Routes

Summary routes lead to less memory usage in routers as their tables contain less routes. Recalculating routes use up CPU on a router. Summary routes prevent recalculation to every part of the network, just the routes directly affected by changes

## Dynamic Routing Protocol Advantages

Routers automatically advertise available subnets to each other without admin having to manually enter every route on every router. Routers will automatically discover changes to the network and update routing tables accordingly

## Dynamic Routing Protocols vs Static Routes

- More scalable
- Using a combination of dynamic routing protocol and static routes is very common in real world environments. In this case, the dynamic routing protocol will be used to carry out the bulk of the work
- Static routes are used on an as needed basis, for example back up purposes

# Routing Protocol Types

Routing protocol types can be split into two main types:
- Interior gateway protocols (IGP) which are used for routing within organization
- Exterior gateway protocols (EGP) which are used for routing between organizations over the internet. The only EGP in use today is **Border Gateway Protocol (BGP)**

## Interior Gateway Protocols

IGPs can be split into two main types:
- Distance Vector routing protocol
- Link state routing protocol

All IGPs do the same job - to advertise routes within an organization and determine the best path
## Distance Vector Routing

- Each router sends its directly connected neighbors a list of all its known networks along with its own distance to each of those networks. It does not have detailed topology information beyond its directly connected neighbors. This type of routing does not advertise the entire network topology
- Distance Vector routing protocols are often called "routing by rumor"

**Routing Information Protocol (RIP)**
**Enhance Interior Gateway Routing Protocol (EIGRP) - Advanced**


## Link State Routing Protocols

- Each router describes itself and its interfaces to its directly connected neighbor. This information is passed unchanged from one router to another
- Every router learns the full picture of the network including every router, its interfaces, and what they connect to

**Open Shortest Path First (OSPF)**
**Intermediate System - Intermediate System (IS-IS)**


`show ip protocol` to check which ip protocol is running
`shop ip section {routing protocol}` to go directly to routing protocol section
`show ip {routing protocol}` show all info obtained from routing protocol 

<span style="color:rgb(255, 0, 0)">
When configuring routing protocols, you will use a wildcard mask which is the opposite of a subnet mask. So a /24 would be 0.255.255.255</span>
# Routing Protocol Metrics

A router may receive multiple possible paths to get to a destination but only the best path will make it into the routing table and be used. 
The different IGPs use different methods to calculate the best path to a destination network

## Metric

- Each possible path is assigned a metric value by the routing protocol which indicated how preferred the path is. The lowest metric value is preferred
- Distance Vector routes advertise to each other the networks they know about and their metric to get to each of them
- Link State routers advertise all the links in their area of the network to each other
- Each router will take this information and make a calculation of its own best path to each destination
- If best path to a destination is lost, it will be removed and replace with the next best route

## RIP Metric - Hop Count 

- RIP uses Hop Count as metric
- The maximum hop count by default is 15. Paths which are more than 15 hops away are deemed as unreachable
- RIP is typically only used in test environments

## OSPF Metric - Cost

OSPF uses Cost as the metric which is automatically derived from the interface bandwidth. You can manually configure the cost of the links if you want to manipulate the path

## IS-IS Metric Cost

IS-IS also uses cost but it is not automatically derived from interface bandwidth. All links have equal cost by default. You can manually configure the cost of the links if you want to manipulate the path. If you do not set the link costs then the path with the lowest hop count will be used

## EIGRP Metric

- EIGRP uses the bandwidth and delay of the links to calculate the metric (Load and reliability can also be considered but are ignores by default)
- A fixed delay value is used based on the interface bandwidth, the protocol does not dynamically measure current delay. You can manually configure the delay on links if you want to manipulate the path

## Choosing a Routing Protocol 

- RIP uses hop count and has a max default metric of 15. Not usually used in production networks because of its scalability limitations
- EIGRP is very simple to maintain, calculates changes very quickly and its metric calculations typically choose the best path by default. However it is only supported on Cisco routers
- OSPF typically choose the best path by default. It is supported by all vendors and is the most commonly deployed IGP today. However, it is more complicated to maintain than EIGRP
- IS-IS links need to be manually configured or it will use hop count to determine the best path

Your choice will likely come down to either EIGRP or OSPF

### Routing Protocol Metric Lab

RIP

```IOS
router rip
network {network address}
no auto-summary
```

OSPF
```IOS
router ospf 1
network {network address} {wildcard mask} area 0
```

EIGRP
```IOS
router eigrp 100
no auto-summary
network {network address} {wildcard mask}
```

Just after configuring a routing protocol, you may not get the expected results immediately. Give the router a minute or so and check paths again 

# Equal Cost Multi Path (ECMP)

 - If multiple paths to a destination have an equal metric, the router will enter all the paths into the routing table. ECMP will load balance the outbound traffic to the destination over different paths
 - All IGP protocols will perform ECMP by default
 - EIGRP is the only routing protocol that is capable of UnEqual Cost Multi Path. It must be manually configured to support this

Important to note that traffic will not be round robin; first packet wont be sent over one path while the second packet is sent over another path. This could cause packets to arrive out of order which could cause some applications to fail

All traffic for a single flow will go over one route. However, if you have a different source host talking to a different destination, that will be load balanced over a different link

# Administrative Distance

- A router will typically only learn routes to a particular destination from a single routing protocol. When multiple routes are learned through a routing protocol, the router will install the path(s) with the best (lowest) routing table
- Different protocols use different methods to calculate this metric
- If paths from the same destination are received from different routing protocols, their metric cannot be compared. For example, a RIP hop count of 5 cannot be compared to an OSPF cost of 60
- The routers must use a different method to chose when routes to the same destination are received from different routing protocols. This is what **Administrative Distance (AD)** is used for.
- The **Administrative Distance (AD)** is a measure of how trusted the routing protocol is. If routes to the same destination are received via different routing protocols, the protocol with the best (lowest) AD wins

## Default AD

![[../attachments/Default Administrative Distance.png]]

## Administrative Distance and Metric

- AD is used to choose between multiple paths learned via different routing protocols. Metric is used to choose between multiple paths learned via the same protocol
- The AD is considered first to narrow the choice down to the single best routing protocol. The Metric is then considered  to choose the best path(s)  which make it into the routing table

in `sh ip route` the first number in the administrative distance. The second number is the metric For example, `[120/1]` would mean that the RIP is being used and that the route has the best (lowest) metric 

## Floating Static Routes

- If the best path to a destination is lost, it will be removed from the routing table and replaced with the next best route. 
- We might want to configure a static route as a backup for the route learned via a routing protocol. The issue with that is static routes default to an AD distance of 1 which will always be preferred over routes learned via an IGP

### Floating Static Routes - OSPF

We can change the AD of a static route to make it acts as a backup rather than the preferred route

Floating static route OSPF example:
`ip route 10.0.1.0 255.255.255.0 10.1.3.2 115` 

115 is a higher AD than OSPF so it will only be used as a backup if OSPF is down

### Floating Static Routes - Static Routes

Floating static can also be used with pure static routing 

`ip route 10.0.1.0 255.255.255.0 10.1.1.2`
`ip route 10.0.1.0 255.255.255.0 10.1.3.2 5`

Instead of load balancing, the first route will be used as the primary route and the bottom route will be used as a backup since the AD value is higher 

# Loopback Interfaces

- Loopback interfaces are logical interfaces. They allow you to assign an IP address to a router or a L3 switch which is not tied to a physical interface. Because they don't have any physical attributes which can fail, loopback interfaces never go down
- Loopback addresses are logical so they can't be physically in the same subnet as other devices, so they are usually assigned a /32 to avoid wasting IP addresses

## Loopback Interface Uses 

- It is best practice to assign a loopback interface to your routers. The loopback is commonly used for traffic that terminated on the router itself. This provides redundancy if there are multiple paths to the router.
- The loopback is also used to identify the router in OSPF

`interface loopback {number}`

# Adjacencies and Passive Interfaces

## Adjacencies

IGP protocols are configured under global config mode and then enabled on each interface. When the routing protocol is enabled on an interface, the router will look for other devices on the link running the same protocol. The router does this by sending out and listening for hello packets through multicast (only routers which are running the same protocol will process the packet). When a matching peer in found, the routers form an adjacency with each other, exchanging routing information

## Passive Interfaces

 - Passive interfaces allow you to include an IP subnet in the routing protocol without sending updates out the interface
 - It is best to configure loopback interfaces as passive interfaces. It is impossible to form an adjacency with a loopback interface because they are not physical interfaces. Making the loopback passive means that it will be advertised by the routing protocol but it will not waste resources sending out and listening for hello packets

### Passive Interface Use Cases

- Loopback interfaces
- When we don't want to send out routing information but we want our internal devices to know about the link (external link)

```IOS
passive-interface {loopback address}
passive-interface {external link}
```

# Route Preference

## Learning Routes

Routers learn routes by:
- An admin configuring IP addresses on its interfaces (connected and local routes)
- Configuring static routes
- Receiving them via a routing protocol

## Router Preference

Routers decide where to forward packets based on the routes it has learned. The best route for a packet decision is based on:
- Longest prefix (most specific route)
- Administrative Distance (AD)
- Metric

If a router learns the exact same network and prefix, it must decide which is the best route. The AD is considered first to narrow the choice down to the single best routing protocol. The Metric is then considered  to choose the best path(s)  which make it into the routing table. If there are multiple best routes with the same AD and Metric, they will both be entered into the routing table and will perform Equal Cost Load Balancing.

This command will show the best route for any particular address:
`show ip route {address}`
## References

