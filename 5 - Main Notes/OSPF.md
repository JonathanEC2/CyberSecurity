OSPF is a link state protocol that supports large networks and has a very fast converge time. It is an open standard protocol that uses Uses Dijkstra’s Shortest Path First algorithm to determine the best path to learned networks.

The process ID is locally significant. It does not have to match on the neighbor router to form an adjacency. However, routers with different process IDs will not learn each others routes


## LSA Flooding 

- Routers create LSAs to tell neighbors about the networks on its interface 
- LSA is then flooded through the network until all routers have received it 
- This results in all the routers in the same area sharing the same Link State Data Base (LSDB)
- LSDBs contain all LSAs router has learned 
- LSA has managing timer of 30 seconds 

### Info in LSA
- Router ID
- IP address 
- Cost
 
# OSPF Areas

An area is a set of routers that share the same LSDB
Each router maintains full information about its own area, but only summary information about other areas

## Backbone Routers

- Routers which have all their OSPF interfaces in Area 0 are Backbone Routers. Routers maintain a full LSDB of other routers and links in their own area
- All OSPF areas must have at least one ABR connected to the backbone area
## Area Border Routers

Ideally each ABR should connect to two areas only, the backbone and another area
ABRs have the following characteristics:
- Separates LSA flooding zones
- Becomes the primary point for area address summarization
- Functions regularly as the source for default routes
- Maintains the LSDB for each area with which it is connected

After manually configuring a router ID, you should restart the OSPF process on the router, as indicated by the message to issue the `clear ip ospf process` command. A running OSPF process will not use a modified router ID until the process is restarted. In addition, OSPF will not send updates to neighbor routers unless there is a topology change. Therefore, changing the router ID by itself will not cause an update to be sent to neighbor routers. You can issue the `clear ip ospf process` command from privileged EXEC mode:

## Autonomous System Boundary Routers (ASBRs) 

- ASBR is an OSPF router that connects OSPF network to the Internet
- The router is running OSPF and redistributing from another source into OSPF. An example would be if we are running EIGRP on the router as well, those routes will be redistributed into OSPF so they will also be advertised through our OSPF neighbors
- Our redistributed routes show up as external route. External route literally means it was redistributed into OSPF 
- Using `default-information originate ` make a router ASBR

# Cost

Routes will be selected based on lowest cost to get to the destination
- For destinations in its own area, a router looks at all available links to get there, and chooses the path with the lowest overall cost
- For destinations in another area, a router looks at all available links to get to the ABR and chooses the path with the lowest cost to the ABR. Its then up to the ABR to choose the best path from there

# OSPF Advanced Topics

## Router ID

- OSPF routers identify themselves using Router ID which is in the form of an IP address
- This will default to being the highest IP address of any loopback interfaces configured on the router, or the highest other IP address if a loopback does not exist
- Loopback interfaces never go down so the Router ID will not change. You can also specify the Router ID
- Interfaces that are down are not eligible to become the Router-ID
- START DR ROUTER FIRST
- If no adjacencies have been formed and a change has been made to the router-id,  you do not need to clear the process or restart the router


Manually configured OSPF Router ID:
```IOS
router ospf
router-id {ip address}
```

Loopback interfaces are configured to operate on their own subnets and are not directly connected to each other. Therefore, the OSPF processes will not form adjacencies if they are the only routes being broadcast
## Passive Interface Configuration

Passive interfaces will be advertised in OSPF so other routers can learn how to get to that network, but the interface itself will not try to form any adjacencies and will not give out any internal information
Make passive interface on connections to neighbors that aren't running OSPF

# OSPF Adjacency

## OSPF Packet Types

- **Hello**: router will send and listen out for hello packets when OSPF is enabled on an interface and form adjacencies with other OSPF routers on the link 
- **DataBase Description (DBD)**: Adjacent routers will tell each other about the networks they know about with the DBD packet
- **Link State Request (LSR)**: If a router is missing information about any of the networks in the received DBD, it will send neighbors an LSR
- **Link State Advertisement (LSA)**: a routing update
- **Link State Update (LSU)**: Contains a list of LSAs which should be updated
- **LSAck**: receiving routers acknowledge LSAs


## OSPF Neighbor States

**Down** - no OSPF neighbor packets have been received
**Init** - Hello packet has been received but the routers ID is not in the Hello packet it received
**2-way** Routers enter each others RID into neighbor table. They are now able to share LSAs to build common  LSDBs
**Exstart** - routers choose which will be master and slave router through DBDs, router with highest ID will become master
**Exchange** - Routers exchange DBDs which contains basic LSA info
**Loading** - Routers send LSR messages to request LSAs they don't have, LSAs are sent is LSUs, They then send LSAck
**Full** - routers have a full OSPF adjacency and identical LSDBs


# OSPF Packet

**Version**: OSPFv2 or OSPFv3
**Type:** 1- Hello, 2- Database Descriptor (DBD), 3- LSR Link State Request, 4- LSU Link State Update, 5- Link State Acknowledgment (LSA Link State Advertisements are inside LSUs)
**Router ID**, and **Area ID**: Of the advertising router, and interface
**Authentication Type**: 0- No Password, 1- Plain-text password, 2- MD5
authentication

### Hello Packets

- OSPF routers discover each other and form adjacencies via Hello packets. They send Hello packets out each interface where OSPF is enables (except passive interfaces)
- Multicast to 224.0.0.5 (all OSPF routers), sent every 10 seconds by default

**Router ID**: 32 bit number that identifies each OSPF router
**Hello Interval**: How often routers send Hello packets, default 10 seconds
**Dead Interval**: How long a router waits to hear from neighbor before declaring it out of service. Default 4x Hello interval
**Neighbors**: list of adjacent OSPF routers that the router has received a Hello packet from
**Area ID**: Area configures to that interface
**Router Priority**: 8 bit number used to select DR of BDR
**DR and BDR IPv4 address**: If known
**Authentication Flags**: Authentication details if configured
**Stub Area Flag**: If the area is a stub area. Stub areas have a default route to their ABR rather than learning routes outside the area

These settings must match for a pair of OSPF routers to form an adjacency:
- Must be in each others neighbor list
- **Hello and Dead Intervals**
- Area ID
- IP subnet
- Authentication Flag
- Stub Area Flag

<span style="color:rgb(255, 0, 0)">The broadcast and point-to-point Open Shortest Path First (OSPF) network types have a default hello timer of 10 seconds and a default dead timer of 40 seconds. The non-broadcast, point-to-multipoint, and point-to-multipoint non-broadcast OSPF network types have a default hello timer of 30 seconds and a dead timer of 120 seconds.</span>

## LSA Types

Type 1: Router LSA (All Routers): Generated by every router, it lists its neighbors and link states within a single area.
Type 2: Network LSA (DR): Generated by the Designated Router (DR) on multi-access networks to describe all routers attached to that segment.
Type 3: Summary LSA (ABR): Generated by Area Border Routers (ABRs) to advertise networks from one area to other areas.
Type 4: ASBR Summary LSA (ABR): Generated by ABRs to inform other areas how to find the Autonomous System Boundary Router (ASBR).
Type 5: Autonomous System External LSA (ASBR): Generated by the ASBR to advertise routes learned from other routing protocols (external to OSPF).

# DR and BDR

On point-to-point links, OSPF routes form FULL adjacency
On multiaccess segments (such as Ethernet) where there can be multiple routers, it is inefficient for all routers to form full OSPF adjacencies with each other

- **DR and BDR Function at the interface level**. A DR and BDR are are elected.
- The router with the highest priority becomes the DR and the router with the second highest priority becomes the BDR. Highest router ID is used in case of a tie, then by the highest loopback IP address, and then by the highest physical IP address.
- Default priority is 1, the higher the better (0/255).


- The DR and BDR establish FULL neighbor state with all routers on the network segment. The neighbor states of other neighbors remain 2-Way and do not directly exchange routes with each other
- When a link state changes on a router connected to a multiaccess segment, it sends a multicast LSU packet to 224.0.0.6 (all designated routers)
- The DR multicasts the update to 224.0.0.5 (all OSPF routers)
- **Only DR and BDRs send out LSAs**
- When a router is neither the DR nor the BDR but is still allowed to participate in the election, the OSPF neighbor state will be reported as DROTHER.

<span style="color:rgb(255, 0, 0)">Set OSPF priority before enabling OSPF </span>

Things to remember

Put loopback interface in OSPF
Only configure internet connectivity on the router connected to the internet

# Configurations

Manually configured OSPF Router ID:
```IOS
router ospf
router-id {ip address}
```

Passive Interface:

Tells router to stop sending out OSPF 'hello' messages
```IOS
router ospf 1
passive-interface {loopback}
passive-interface {interface}
```

Default Route Injection:
```IOS
ip route 0.0.0.0 0.0.0.0 {next hop address}
router ospf 1
default-information originate
```

Network:
```
network {network address} {wildcard mask} {area}
```

Manual Summarization:
```
router ospf 1
network 10.1.0.0 0.0.255.255 area 0
network 10.0.0.0 0.0.255.255 area 1
area 0 range 10.1.0.0 255.255.0.0
area 1 range 10.0.0.0 255.255.0.0
```

Reference Bandwidth:
```IOS
router ospf 1 
auto-cost reference-bandwidth 100000
```

Manipulating Cost
```IOS
interface {interface}
ip ospf cost 50
```

OSPF Priority for BR and BDR:
```IOS
interface {interface}
ip ospf priority {number}
```