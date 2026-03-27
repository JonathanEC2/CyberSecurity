2026-03-25 22:20
Tags: [[]]

# DNS

- DNS resolves a FQDN such as www.cisco.com to an IP address
- Enterprises will typically have an internal DNS server which can resolve the IP address of internal hosts. Hosts will send their DNS queries to this server. If the internal DNS server cannot resolve said query, it will forward the request out to the public DNS server on the Internet
- UDP port 53 (can fail over to TCP)
- **Normal DNS does not form a TCP connection**

## Router DNS Commands

`ip domain-lookup` allows a router to be able to resolve hostnames
`ip name-sever` configures a router or device to use specific DNS servers for resolving hostnames to IP addresses

**DNS Server:**
```IOS
ip domain-lookup
ip name-server 172.23.4.1
ip domain-name flackbox.lab (primary domain name)
ip dns server
ip host LinuxA 172.23.4.2
```

**DNS Client:**
```IOS
ip domain-lookup
ip name-server 172.23.4.1
ip domain-list flackbox.lab (additinal suffixes to search)
```

# ARP Address Resolution Protocol

- Sender needs to know the receivers IP and MAC address to form the packet its going to send. We can point the sender directly to the destination IP address or to the FQDN
- DNS maintains a mapping of FQDNs to IP addresses
- ARP is used to map the IP addresses to MAC addresses

ARP replies are saved in a hosts ARP cache so it doesn't need to send an ARP request every time it wants to communicate
## References
