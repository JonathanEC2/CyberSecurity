2026-03-05 15:04
Tags: [[]]

# IPv4 Address Exhaustion and NAT

[[1 - Source Material/Section 8. Subnetting#Private IP Addresses|Private Addresses]]

[[1 - Source Material/Section 8. Subnetting#IPv6|IPv6 and NAT]]

# Static NAT

Permanent one-to-one mapping usually between a public and private IP address. Used for servers which must accept incoming connections

```
int {}
ip nat outside

int {}
ip nat inside

(global) ip nat inside source static {inside local ip} {inside global ip}
```

`sh ip nat translation`

# NAT Translation

![[attachments/Pasted image 20260305203018.png]]

- **Inside Local Address** - The IP address actually configured on the inside hosts OS
- **Inside Global Address** -  The NAT'd address of the inside host as it will be reaches by the outside network (if someone is outside the network sending traffic in, what address are they going to be using as their destination address)
- **Outside Local Address** - The IP address of the outside host as it appears to the inside network (if you are on an internal server and sent some traffic to the outside, what IP address would you use)
- **Outside Global Address** - The IP address assigned to the host on the outside network by the hosts owner

## Outside Local vs Outside Global

For one way NAT, the Outside Local and Outside Global address will be the same

# Dynamic NAT

Uses a pool of public IP address that are given out as an as needed, first come first serve basis. Usually used for internal hosts which need to connect to the Internet but do not need to accept incoming connections

Since traffic is always initiated by internal hosts, they do not need to have a fixed public IP address with a static NAT. They do need outbound connectivity to the Internet so they need to be translated to a public IP address

With standard dynamic NAT you need a public IP address for every inside host which need to communicate with the outside. When all addresses in the pool are used, new connections from other inside hosts will fail because there are no addresses left to translate them. They will have to wait for an existing connection to be torn down

## Dynamic NAT Configuration

```
int {}
ip nat outside
int {}
ip nat inside
```

Configure pool of global addresses:
`ip nat pool Flackbox {begin ip pool} {end ip pool} netmask {}`

Create an access list that references the internal IP addresses we want to translate:
`access-list 1 permit {ip address} {wildcard mask}`

Associate the access list with the NAT pool to complete the configuration:
`ip nat inside source list 1 pool Flackbox`

## `clear ip nat translation`

`clear ip nat translation` can be used to remove translations from the translation table
It is often required if you want to edit you NAT configuration - the router will not allow changes when there are active translations
`clear ip nat translation *` will remove all dynamic translations

`sh ip nat statistics`

# Port Address Translation 

- Allows the same IP address to be used multiple times for translations. You do not need a public IP address for every inside host
- The router tracks translations by IP address and Layer 4 port number. Because different inside hosts are assigned different port numbers, the router knows which host to send return traffic to even when the public IP address is the same

## Dynamic NAT with Overload

- Dynamic NAT with Overload uses PAT to allow more clients to be translated than IP address are available in the NAT pool
- The router keeps track of source ports in the translation table. When the return traffic is sent back, the router checks the destination port number to see which host to forward it to

## Dynamic NAT with Overload

Same config as standard dynamic NAT except when you associate the access list to the NAT pool, you add the `overload` command

Associate the access list with the NAT pool to complete the configuration:
`ip nat inside source list 1 pool Flackbox overload`

## PAT with Single IP address

- Small offices typically do not purchase a range of IP addresses. They will get their IP address via DHCP. ISP can not guarantee that you will get the same IP address every time which is an issue when it comes to NAT
- PAT can be used to allow multiple inside hosts to share the single outside public IP address
- The configuration is very similar to Dynamic NAT with Overload but translates to the outside interface address rather than a pool of addresses since the DHCP address can change


```
int {}
ip nat outside
int {}
ip nat inside
```


Create an access list that references the internal IP addresses we want to translate:
`access-list 1 permit {ip address} {wildcard mask}`

Associate the access list with the interface receiving the DHCP IP address
`ip nat inside source list 1 interface {} overload`
## References
