2026-03-25 17:41
Tags: [[]]

<span style="color:rgb(255, 0, 0)">Devices cannot communicate with other devices if they are not directly connected in the same subnet and do not have a route to each other</span>
# Static Routes

If a router receives traffic for a network that it **isn't directly connected** to, it needs to know how to get the traffic there in order to forward the traffic
An admin can manually add a static route to the destination or the router can learn it via a routing protocol

`ip route { target network ip address} {subnet mask} {next hop ip address}`

### Types of static route

Fully specified - Includes the interface:
`ip route 10.1.1.0 255.255.255.0 gigabitethernet0/1 192.168.1.1`

Directly attached  - specifies the destination IP and the outbound interface:
`ip route 10.1.1.0 255.255.255.0 gigabitethernet0/1`

Recursive - what is used most times:
`ip route 10.1.1.0 255.255.255.0 192.168.1.1`

# Summarization, Longest Prefix Match, and Default Routes

## Summarization

For static routes, summary routes lessen administrative overhead and memory usage on other routers. Only works when routes are in contiguous ranges

## Longest Prefix Match

When there are overlapping routes, the longest prefix will be selected; the more specific route will be selected (255.255.255.0 is a longer prefix than 255.255.0.0)

## Router Preference

Routers decide where to forward packets based on the routes it has learned. The best route for a packet decision is based on:
- Longest prefix (most specific route)
- Administrative Distance (AD)
- Metric

## Load Balancing

When multiple equal lengths are added for the same destination, the router will add them all to the routing table and load balance them

<span style="color:rgb(255, 0, 0)">Load balancing has to be done both ways</span>

## Default Route (Gateway of Last Resort)

To add a route that we don't have a specific route for, we will use `0.0.0.0 0.0.0.0 {next hop}`. This is used as a catch all for any traffic that doesn't match one of our more specific routes. <span style="color:rgb(255, 0, 0)">When a router receives a packet with a destination address not found in its routing table, it will use the default route to forward the packet. </span>
## References
