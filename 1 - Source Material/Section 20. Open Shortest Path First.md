
# OSPF Characteristics

Link state protocol
It supports large networks and has a very fast converge time
Messages are sent using multicast 
Open standard protocol

## OSPF vs EIGRP vs RIP

OSPF is most commonly used
- Is supports large networks and has always been open standard. It is supported on all vendors equipment.
- EIGRP can be simpler to implement and troubleshoot. It was historically a Cisco proprietary protocol but it is now an open standard. However, there is still limited support on other vendors equipment

## Link State Routing Protocol

- Each router describes itself and its interfaces to its directly connected neighbor. This information is passed unchanged from one router to another
- Every router learns the full picture of the network including every router, its interfaces, and what they connect to
- OSPF routers use Link State Advertisements (LSA) to pass on routing

## OSPF Operations

1. Discover neighbors
2. Form adjacencies
3. Flood Link State Database  (LSDB) 
4. Compute shortest path 
5. Install best routes in routing table
6. Respond to network changes

## OSPF Packet Types

- **Hello**: router will send and listen out for hello packets when OSPF is enabled on an interface and form adjacencies with other OSPF routers on the link 
- **DataBase Description (DBD)**: Adjacent routers will tell each other about the networks they know about with the DBD packet
- **Link State Request (LSR)**: If a router is missing information about any of the networks in the received DBD, it will send neighbors an LSR
- **Link State Advertisement (LSA)**: a routing update
- **Link State Update (LSU)**: Contains a list of LSAs which should be updated
- **LSAck**: receiving routers acknowledge LSAs

# OSPF Basic Configuration

## OSPF Configuration
### Process ID

``` IOS
router ospf {process ID}
```

- Different interfaces on a router can run different instances of OSPF. Different instances have different Link State Databases
- Only one instance is typically configured on OSPF routers, multiple process IDs are rarely used
- The process ID is locally significant. It does not have to match on the neighbor router to form an adjacency. However, routers with different process IDs will not learn each others routes

### Network 

```IOS
router ospf
network 10.0.0.0 0.0.255.255
```

- The network command will use a wildcard mask which is the inverse of a subnet mask. **Subtract each octet in the subnet mask from 255 to calculate the wildcard mask (255- octet number)**
- A subnet mask of 255.255.0.0 equals a wildcard mask of 0.0.255.255. A subnet mask of 255.255.255.252 equals a wildcard mask of 0.0.0.3
- You must enter a wildcard mask

The network command means:
- Look for interfaces with an IP address which falls within this range
- Enable OSPF on those interfaces - send out and listen for OSPF hello messages, and peer with the adjacent OSPF routers
- <span style="color:rgb(255, 0, 0)">Advertise the network and mask which is configured on those interfaces</span>

## OSPF Verification

`sh run | section ospf`
`sh ip ospf interface brief`

| Operation                                                            | Command                 |
| -------------------------------------------------------------------- | ----------------------- |
| 1. Discover neighbors <br>2. Form adjacencies                        | `show ip ospf neighbor` |
| 3. Flood Link State Database  (LSDB)                                 | `show ip ospf database` |
| 4. Compute shortest path <br>5. Install best routes in routing table | `show ip route`         |
| 6. Respond to network changes                                        |                         |

# OSPF Advanced Topics

- OSPF routers identify themselves using Router ID which is in the form of an IP address
- This will default to being the highest IP address of any loopback interfaces configured on the router, or the highest other IP address if a loopback does not exist
- Loopback interfaces never go down so the Router ID will not change. You can also specify the Router ID
- **Best practice is to use a loopback address or manually set the router** 
-  If a loopback or higher IP address is configured after EIGRP has been set up, **the router ID will change on OSPF process restart**

Manually configured OSPF Router ID:
```IOS
router ospf
router-id {ip address}
```

## Passive Interface Configuration

Passive interfaces will be advertised in OSPF so other routers can learn how to get to that network, but the interface itself will not try to form any adjacencies and will not give out any internal information

```IOS
router ospf 1
passive-interface {loopback}
passive-interface {interface}
```

If more of your interfaces are passive rather than active, you can set passive as the default:
`passive-interface default`

## Default Route Injection

When you have a default static route for all traffic going out to the Internet, you don't want to manually configure a default static route on every router. What we do is configure a default static route on the final outbound router which is connected to the Internet, advertise it, and inject it into RIP so all internal routers learn about it automatically

```IOS
ip route 0.0.0.0 0.0.0.0 {next hop address}
router ospf 1
default-information originate
```

**If you want your routers to have a route to the external network (internet), you must configure that network statement on the border router (12:10)**

# OSPF Areas

Every router learns the full picture of the network including every router, its interfaces, and what they connect to. This can cause issues in large networks: 
- Too many routes can use up too much memory
- Network changes can cause all routers to reconverge which takes time and CPU resources

OSPF supports a hierarchical design that segments large networks into smaller areas to solve this problem. Each router maintains full information about its own area, but only summary information about other areas

A two level hierarchy is used: 
- Transit area (backbone area or area 0) does not generally contain end users
- Regular area (non-backbone area) used to connect end users to the transit area. By default, all traffic goes through transit area
- All routers can be in area 0 in a small network

## Network

```
network {network address} {wildcard mask} {area}
```

The area is configured at the interface level with the network command. For a router to form an adjacency, its neighbor must be in the same area

## Backbone Routers

Routers which have all their OSPF interfaces in Area 0 are Backbone Routers. Routers maintain a full LSDB of other routers and links in their own area

## Internal (Intra Area) Routes 

Routes received from other routers in the same area appear as Internal OSPF routes

## OSPF Router Types
### Area Border Routes (ABR)

Routers that have interfaces in multiple areas are Area Border Routes

ABRs have the following characteristics:
- Separates LSA flooding zones
- Becomes the primary point for area address summarization
- Functions regularly as the source for default routes
- Maintains the LSDB for each area with which it is connected

Ideally each ABR should connect to two areas only, the backbone and another area

#### Manual Summarization 

ABRs do not automatically summarize. If you do not configure summarization, all routes are flooded everywhere

Ex:
```IOS
router ospf 1
network 10.1.0.0 0.0.255.255 area 0
network 10.0.0.0 0.0.255.255 area 1
area 0 range 10.1.0.0 255.255.0.0
area 1 range 10.0.0.0 255.255.0.0
```


### Inter Area (IA) Routes

Routes that are shared between different OSPF areas. These are typically summary routes that are advertised by an ABR

### Normal Area Routers

Routers that have all their interfaces in one normal area
Routers maintain a full LSDB of other routes and link in their own area. They learn Inter Area routes to other areas from their ABRs

### Autonomous System Boundary Routers ASBRs 

The router is running OSPF and redistributing from another source into OSPF. An example would be if we are running EIGRP on the router as well, those routes will be redistributed into OSPF so they will also be advertised through our OSPF neighbors

Our redistributed routes show up as external route. External route literally means it was redistributed into OSPF 