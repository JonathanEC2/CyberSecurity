2026-01-08 19:36
Tags: [[]]

# Connected and Local Routers

A router has two main functions:
- Determining the best path to available networks
- Forwarding traffic to those routers

- The best available path(s) to a destination are listed in the routers routing table and will be used for forwarding traffic. Only the best path(s) are stored
- A routing table consists of directly connected networks and routes configured statistically by the admin or dynamically learned through a routing protocol


## show ip route 

`sh ip route`

Connected routes are automatically entered into the routing table
From IOS 15, local routes will also be added to the routing table. Local routes always have a /32 mask and show the IP address configured on the interface

# Static Routes

If a router receives traffic for a network that it **isn't directly connected** to, it needs to know how to get the traffic there in order to forward the traffic
An admin can manually add a static route to the destination or the router can learn it via a routing protocol

`ip route { target network ip address} {subnet mask} {next hop ip address}`

# Summarization, Longest Prefix Match, and Default Routes

## Summarization

For static routes, summary routes lessen administrative overhead and memory usage on other routers. Only works when routes are in contiguous ranges

## Longest Prefix Match

When there are overlapping routes, the longest prefix will be selected; the more specific route will be selected (255.255.255.0 is a longer prefix than 255.255.0.0)

## Load Balancing

When multiple equal lengths are added for the same destination, the router will add them all to the routing table and load balance them

<span style="color:rgb(255, 0, 0)">Load balancing has to be done both ways</span>

## Default Route (Gateway of Last Resort)

To add a route that we don't have a specific route for, we will use `0.0.0.0 0.0.0.0 {next hop}`. This is used as a catch all for any traffic that doesn't match one of our more specific routes. 

# Lab Info

The way that traffic originating from the router itself works is it uses the exit interface as the IP address. 

You can use extended ping command by just typing `ping` 

For load balancing to work, prefixes must be the exactly the same. The way the load balancing algorithm works is that its based on a hash between the two different hosts.  So traffic from one host to another host between the same two IP addresses of the same port is always going to go over the same path. This is to keep the same flow which prevents packets from arriving out of order.

## References
