2026-02-11 20:23
Tags: [[]]

# Dynamic Host Configuration Protocol (DHCP)

- A client server protocol that automatically provides a host with its IP address and other configuration information such as subnet mask and default gateway
- DHCP clients obtain their IP configuration info from a DHCP server rather than being manually configured

(D)iscover (O)ffer (R)equest (A)cknowledge

## DHCP Benefits - Reduced Network Admin

- Centralized and automated IP configuration
- Can assign different IP configuration values 
- Efficient handling of clients that must be updated frequently such as laptops that move to different locations on a network
- The forwarding of initial DHCP messages by using a **DHCP relay agent** which eliminates the need for a DHCP server on every subnet


DHCP minimizes configuration errors caused by manual IP address configuration such as typos or  address conflicts

## DHCP Clients

- Desktops are good candidates to be DHCP clients because there will typically be many of them in an office and would save time on manual configuration. DHCP Clients do not accept incoming connections so it does not matter if their IP address changes

- Servers and network infrastructure devices such as routers and switches will typically not be DHCP clients. They are mission critical devices which do not move and are required for the network to function. Their IP addresses are manually configured to ensure they will not change and are not dependent on DHCP

# Cisco DHCP Server

## Cisco DHCP Server Configuration

Most likely used in a small network where you don't want the expense of putting in a dedicated server to act as a DHCP server. Instead you can just use a Cisco router

Typically you will have IP addresses that you will want to be fixed such as printers, routers, or infrastructure devices. Therefore you will not give out every single IP address. You'll usually have the reserved addresses either at the start of the scope or at the end of the scope,

```IOS
ip dhcp excluded-address {address range}
ip dhcp pool {name}
network {network} {subnet mask }
default-router {router ip}
dns-server {dns server ip}
```

`show ip dhcp binding` to see what address were give out and who they were given to
# External DHCP Server

- Routers do not forward broadcast traffic by default. A client that sends our a DHCP request will hit the router, but the router will drop the packet. Therefore if the DHCP server is on another subnet, the request will never reach the DHCP server
- You will need to configure the router to forward DHCP requests. You will configure it on the interface which will be receiving the DHCP request
```IOS
interface {interface}
ip helper-address {dhcp server}
```
# Windows, Mac, and  Linux Client IP Settings


# Cisco DHCP Client

## Configuring a Cisco Router as a DHCP Client

Cisco routers are typically manually configured with a static IP address. An exception to this is where an office is connected to the Internet but has not bought static public IP addresses. The office still requires at least one public IP address to allow internal hosts outbound connectivity to the Internet via NAT. In this case, the router will receive the public IP address on its outside interface from the Internet service provider via DHCP

```
interface {interface}
ip address dhcp
no shutdown
```

`dhcp lease`
Show ip dhcp binding
## References
