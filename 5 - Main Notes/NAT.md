2026-03-26 21:20
Tags: [[]]

```
int {}
ip nat outside

int {}
ip nat inside

(global) ip nat inside source static {inside local ip} {inside global ip}
```

# NAT Translation


![[attachments/Pasted image 20260305203018.png]]

- **Inside Local Address** - The IP address actually configured on the inside hosts OS
- **Inside Global Address** -  The NAT'd address of the inside host as it will be reaches by the outside network (if someone is outside the network sending traffic in, what address are they going to be using as their destination address)
- **Outside Local Address** - The IP address of the outside host as it appears to the inside network (if you are on an internal server and sent some traffic to the outside, what IP address would you use)
- **Outside Global Address** - The IP address assigned to the host on the outside network by the hosts owner

# Dynamic NAT

Uses a pool of public IP address that are given out as an as needed, first come first serve basis. Since traffic is always initiated by internal hosts, they do not need to have a fixed public IP address with a static NAT.

With standard dynamic NAT you need a public IP address for every inside host which need to communicate with the outside. When all addresses in the pool are used, new connections from other inside hosts will fail because there are no addresses left to translate them.

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

# Port Address Translation (Dynamic NAT with Overload)

- Allows the same IP address to be used multiple times for translations. You do not need a public IP address for every inside host
- The router tracks translations by IP address and Layer 4 port number. Because different inside hosts are assigned different port numbers, the router knows which host to send return traffic to even when the public IP address is the same

Same config as standard dynamic NAT except when you associate the access list to the NAT pool, you add the `overload` command

Associate the access list with the NAT pool to complete the configuration:
`ip nat inside source list 1 pool Flackbox overload`

## PAT with Single IP address

PAT can be used to allow multiple inside hosts to share the single outside public IP address

```
int {}
ip nat outside
int {}
ip nat inside
```

YOU WILL NOT CREATE POOL

Create an access list that references the internal IP addresses we want to translate:
`access-list 1 permit {ip address} {wildcard mask}`

Associate the access list with the interface receiving the DHCP IP address
`ip nat inside source list 1 interface {} overload`

## References
