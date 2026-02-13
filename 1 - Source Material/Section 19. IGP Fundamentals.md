
2026-01-28 20:08
Tags: [[]]

# Routing Information Protocol

## RIP Characteristics

- Distance Vector protocol
- Uses hop count as its metric, maximum hop count is 15
- Equal Cost Multi Path for up to 4 paths by default

## RIPv2 vs RIPv1

- RIPv1 does not support VLSM
- RIPv1 updates are sent every 30 seconds via broadcast address. RIPv2 uses multicast address 224.0.0.9
- RIPv2 supports authentication, RIPv1 does not. With authentication, we can put a password on both sides of the link so they will not form an adjacency unless the passwords match

## RIPv2 Configuration

```IOS
router rip
version 2
network {network address}
```

## Auto-Summary

- RIP will automatically summarize routes to the classful boundary by default. For example, 192.168.10.1/30 will be advertised as 192.168.10.0/24. 172.16.10.1/30 will be advertised as 172.16.0.0/16
- This is almost never desirable, so you should turn it off using `router rip` then `no auto-summary`

## Manual Summarization

- Gives you control of how you summarize. The individual summarized routes are not advertised, only their summary routes
- You configure this at the interface level and you configure it on the interface you are sending it out of

```IOS
interface {interface}
ip summary address rip {ip address} {subnet mask}
```

## RIPv2 Verification 

`show ip protocol`
`sh run | section rip
`show ip route`
`show ip rip database`

## Default Route Injection

When you have a default static route for all traffic going out to the Internet, you don't want to manually configure a default static route on every router. What we do is configure a default static route on the final outbound router which is connected to the Internet, advertise it, and inject it into RIP so all internal routers learn about it automatically

```IOS
ip route 0.0.0.0 0.0.0.0 {next hop address}
router rip
default-information originate
```

# RIP Lab

**If you want your routers to have a route to the external network (internet), you must configure that network statement on the border router (12:10)**
# EIGRP 

## EIGRP Characteristics

- Advanced Distance Vector protocol
- It supports large networks and has a very fast converge time
- Network topology changes are only sent to routers affected by the change
- Messages are sent using multicast
- EIGRP will automatically perform Equal Cost Load Balancing on up to 4 paths by default. This can be increased up to 32 paths (platform dependent)
- EIGRP can also perform UnEqual Cost Load Balancing

## EIGRP Configuration 

### Autonomous System (AS) number

`router eigrp 100`

100 is the example is the Autonomous System (AS), meaning an independent administrative domain. EIGRP routes need to have the same AS number to peer with each other

### Network

```IOS
router eigrp 100
network 10.0.0.0 0.0.255.255
```

- The network command will use a wildcard mask which is the inverse of a subnet mask. **Subtract each octet in the subnet mask from 255 to calculate the wildcard mask (255- octet number)**
- A subnet mask of 255.255.0.0 equals a wildcard mask of 0.0.255.255. A subnet mask of 255.255.255.252 equals a wildcard mask of 0.0.0.3
- If you do not enter a wildcard mask, the command defaults to using the classful boundary wildcard mask

The network command means:
- Look for interfaces with an IP address which falls within this range
- Enable EIGRP on those interfaces - send out and listen for EIGRP hello messages, and peer with the adjacent EIGRP routers
- <span style="color:rgb(255, 0, 0)">Advertise the network and mask which is configured on those interfaces</span>

## EIGRP Router ID

- EIGRP routers identify themselves using Router ID which is in the form of an IP address
- This will default to being the highest IP address of any loopback interfaces configured on the router, or the highest other IP address if a loopback does not exist
- Loopback interfaces never go down so the Router ID will not change. You can also specify the Router ID
- **Best practice is to use a loopback address or manually set the router** 
- If a loopback or higher IP address is configured after EIGRP has been set up, **the router ID will change on EIGRP process restart**

Manually configured EIGRP Router ID:
```IOS
router eigrp 100
eigrp router-id {ip address}
```

`show ip eigrp neighbors`
`show ip route`
`sh run | section eigrp`
`show ip protocol`
`show ip eigrp interfaces`


## References
