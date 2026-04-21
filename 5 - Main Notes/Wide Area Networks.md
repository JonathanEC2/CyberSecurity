2026-04-06 20:14
Tags: [[]]

# Wide Area Network

 A WAN is a geographically distributed network that connects multiple Local Area Networks together

# VPN

A Virtual Private Network provides a virtual tunnel between private networks across a shared public network such as the Internet. Traffic traveling across the tunnel is encrypted and only readable by the authorized used on both sides.

## Site to Site VPN

Site-to-site VPNs are terminated on a router or firewall. They generally use IPsec for encryption

- IPsec Tunnel: open standard IPsec tunnel, does not support multicast
- **General Routing Encapsulation (GRE) over IPsec Tunnel:** adds support for multicast (useful for advertising routing protocols)
- **Dynamic Multipoint VPN (DMVPN)**: Cisco proprietary. Scalable simple hub and spoke style config enables full mesh connectivity between all offices
- **Group Encrypted Transport VPN** (GETVPN): Scalable centralized policy for VPN over nonpublic infrastructure (ex. MPLS)


## IPsec

- Open standard framework that provides secure encrypted communication on an IP network
- **Internet Key Exchange (IKE)** handles negotiation of protocols and algorithms, and generates the encryption and authentication keys
- **Internet Security Association and Key Management Protocol (ISAKMP)** defines the procedures for authenticating and communicating peer creation and management of Security Associations. Typically uses IKE for key exchange

- **Authentication Header (AH)** provides integrity, authentication, and protection from replay attacks
- **Encapsulating Security Payloads (ESP)** provides confidentiality, integrity, authentication and protection from replay attacks. ESP is more commonly used

## ESP Tunnel Mode

- Tunnel mode protects the internal routing info by encrypting the IP header of the original packet. The original packets is encapsulated by another set of IP headers
- Widely implemented in site-to-site VPNs

## ESP Transport Mode

Encrypts only the payload and ESP trailer; so the IP header of the original packet is not encrypted
This mode is usually used when another tunneling protocol (GRE/L2TP) is used to first encapsulate the IP data packet, them IPsec is used to protect the GRE/L2TP
Implemented in client to site VPN

## IPSec VPN Configuration

Interesting Traffic: VPN devices recognize which traffic to protect
ISAKMP/IKE Phase 1: VPN devices negotiate an IKE security policy, authenticate each other and establish a secure channel
ISAKMP/IKE Phase 2: The VPN devices negotiate an IPsec security policy to protects IPsec data
Data Transfer: The VPN devices apply security services to traffic, then transmit the traffic

### Site to Site VPN Cryptography

- Use symmetric encryption algorithms such as DES, 3DES and AES to send encrypted traffic between locations over an untrusted network such as the Internet
- Traffic inside an office is often unencrypted as it is seen as a trusted network
-  A preshared key can be used but certificates are better as they are more scalable

## Remote Access VPN

- These connections are between router or firewall in the office and VPN software installed on an individual user's device
- The users can access the VPN from anywhere with Internet connectivity
- They usually use SSL (Sometimes IPsec) for encryption

### Split Tunneling

- Corporate traffic goes over VPN tunnel to the corporate site
- Public traffic will go directly to Internet, not through tunnel
- Better performance

### Full Tunnel

- All traffic go over VPN tunnel, but is redirected to Internet web server
- Allows you to enforce security policy on staff

# Leased Lines

Dedicated physical connection between two locations
It has fixed reserved bandwidth which is not shared by anyone else. The bandwidth is the same in both directions
Leased lines are expensive and have a long lead time for installation

![[attachments/Pasted image 20260308225701.png]]

# Multi Protocol Label Switching

- Traffic from multiple customers can travel over the providers shared MPLS network so this it is a VPN service
- Different SLAs for uptime and delay are offered at different price points
- Use Ethernet connections
- MPLS provides full mesh topology by default

## Layer 3 MPLS VPN

![[attachments/Pasted image 20260309191101.png]]

CE: Customer Edge
PE: Provider Edge
P: Provider Core device

- MPLS run across the providers core on the PE and P routers
- The customer CE routers do not run MPLS
- The customer CE routers peer at Layer 3 with the providers PE routers
- Static routes or routing protocol run between the CE and PE
- The PE router looks like another customer router to the customer. The providers core routers are transparent to the customer

## Layer 2 MPLS VPN

The CE devices do not peer with the PE devices. The entire provider network is transparent to the customer
The provider network acts like a giant switch. **The customer sites are in the same IP subnet**
This may be required for clustering an application over the WAN

- **Virtual Private LAN Service (VPLS)**: multipoint L2 VPN
- **Virtual PseudoWire Service (VPWS)**: point to point L2 VPN

## Internet Redundancy Options

![[attachments/Pasted image 20260309194309.png]]
## References
