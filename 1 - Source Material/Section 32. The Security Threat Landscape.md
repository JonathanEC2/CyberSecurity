2026-03-09 20:01
Tags: [[]]

# The Security Threat Landscape

Threat: has potential to cause harm to an IT asset
Vulnerability: a weakness that compromise the security or functionality of a system
Exploit: uses a weakness to compromise the security or functionality of a system
Risk: the likelihood of an attack
Mitigation: techniques to eliminate or reduce the potential and seriousness of an attack

## Malware

Virus- inserts itself into software and can span from computer to computer, requires human interaction
Worms - self propogate
Trojan horse
Ransomware

## Hacking Tools 

Password cracking tools
Sniffers - see data going across network
Ping sweepers - reconnaissance to see what devices are alive within a network
Port and vulnerability scanners

## Script Kiddies and Targeted Attacks

Pejorative term for low skilled attackers who download and use  off-the-shelf hacking software to launch exploits
They will typically attempt to exploit any vulnerable host they can connect to. Their attacks are mostly not targeted against an individual or organization

## Targeted Attacks

This attack is rarer
Skilled attackers will typically start off with very stealthy and low impact reconnaissance, and systematically escalate the attack from there


# Common Attacks

## Reconnaissance

Obtains info about the intended victim
Will typically start with passive methods such as searching whois information, phone directories, job listings, etc.
They will then dig deeper using ping sweeps, port and vulnerability scanners

## Social Engineering

Uses deception to manipulate individuals into giving out confidential or personal information

## Phishing 

Attacker pretends to be someone else over email to reveal personal info such as passwords and credit card information

## Data Exfiltration

Data leaves an organization without authorization, can intentional or accidental

## DoS

prevents legit users from accessing an IT resource. Floods the target system with more info than it can handle

### TCP Syn Flood Attack

Attacker send numerous SYN packets, server responds with a SYN/ACK packet but the attacker never sends the ACK packet to complete the handshake

### Reflection and Amplification Attacks

Reflection is a DoS attack where the attacker spoofs the victims source address. Enough of the return traffic back to the victim can bring the victim down 
Amplification causes a large amount of response traffic to the victim
## DDoS

Dos from multiple sources using a botnet
Infected hosts connect to the attackers command and control server. This evades firewalls because the connection is initiated from the inside

## Spoofing 

Spoofing types includes:
- IP address spoofing 
- MAC address spoofing
- Application spoofing

## Man in the Middle Attack

Attacker inserts themselves into a communication path between legit hosts

## Buffer Overflow

malformed and/or too much data to the target system. This can cause a DoS or compromise the target system

# Firewalls and IDS/IPS

## IDS and IPS

- Uses signatures to inspect packets up to Layer 7 of the OSI stack looking for traffic patterns which match known attacks
- They can also use anomaly based (heuristic ) inspection to look for unusual behavior
- IDS sits **along side** traffic flow and informs security administrators of any potential concerns. Will use port mirroring to send a mirror copy to the IDS
- IPS sits **inline** with traffic flow and can also block attacks. IPS can be a bottleneck

## IPS vs Firewalls

- Uses signatures to inspect packets up to Layer 7 of the OSI stack looking for traffic patterns which match known attacks
- Firewalls block or permit traffic based on rules such as destination IP and port number (similar to ACL)
- Organizations always deploy firewalls on the Internet edge
- IPS's are options which may be deployed in conjunction with a firewall

 Next Generation Firewalls often also have IPS capability. They are also often capable of acting as the endpoint of VPN tunnels

## Example Topology

![[attachments/Pasted image 20260309210002.png]]

# Firewalls vs Packet Filters

## Stateful Firewalls

- Maintains a connection table which tracks the two-way 'state' of traffic passing through the firewall
- Return traffic is permitted by default. This would override a 'deny all traffic' rule for legit return traffic

## Next Generation Firewalls

- These move beyond port/protocol inspection and blocking to add application-level inspection, intrusion prevention, and user based activity
- Deep packet inspection on packets up to Layer 7 (tradition firewall had inspection only up to Layer 4)
- Different permissions can be applied to different users
- Cisco ASA with FirePower

## How Packet Filters Works

- An ACL security policy is a packet filter
- Does not maintain a connection table
- They affect traffic in one direction only and do not track the state of two way connection going through the router

## Internal and External Threats

- ACL packet filters and firewalls are part of an overall defense in depth strategy
- Use firewalls on major security boundaries and augment this with internal ACLs
- Purely external threats are primarily covered with strong firewall and IPS protection on the network perimeter
- Sensitive hosts should have firewall and IPS protection from internal hosts

# Cryptography

Transforms readable messages into unintelligible form and then later reverses the process
Uses authentication and encryption methods

Cryptography provides these services:
- Confidentiality
- Integrity
- Authenticity
- Non-repudiation

## Symmetric Encryption

- Same shared key both encrypt and decrypt. Shared key is known by both sender and receiver and must be kept secret
- Fast, Used for large transmissions
- DES, 3DES, AES, SEAL

## Asymmetric Encryption

- Private and public key pairs
- Data encrypted with the public key can only be decrypted with the private key and vice versa
- Only the private key must be kept secret
- Slow, used for smaller transmissions (symmetric key exchange, digital signatures)
- RSA, DSA

## Hash-Based Message Authentication Codes (HMAC)

- Provides data integrity
- The sender creates a hash value from the data to be sent using a symmetric key. The hash value is appended to the data. The receiver hashes the data with the same shared key. If the hash values are the same, the data has not been altered in transit
- Used for large transmissions
- MD5, SHA

## Key Distribution

For symmetric encryption, both sides need to know the shared key. This leads to a key distribution problem because it is not secure too send the shared key over the same channel as the data you want encrypted

## Public Key Infrastructure

- Solves distribution problem
- It uses a trusted introducer (Certificate Authority) for the two parties who need secure communication
- Both parties need to trust the CA

# Transport Layer Security (TLS)

- SSL deprecated, TLS is the successor
- Can be used to provide secure web browsing with HTTPS
- Uses symmetric cryptography to encrypt transmitted data. Symmetric keys are generated uniquely for each connection
- Authentication is provided by public key cryptography
- MAC provides integrity

## HTTPS Example

**Website**:
Website will generate a public and private key pair. Website would then send a Certificate Request (CR) including their public key to the CA. CA will then ask for out of band verification (ex. telephone) to prove CAs identity. Once verifies, CA will generate a certificate for the website which contains the websites public key and is signed by the CA.

**User**:
Through PKI, your web browser trusts the CA and has a copy of their public key that is built into your browser. When you open the website, the website will send you their certificate which has been signed by a CA. Browser then verifies it is a valid certificate. You trust certificate because you  trust CA.

You still are not sure at this point if you are communicating with the website yet because other people that have accessed that website also have been sent the certificate. You know the certificate is valid but don't know it is the actual website you are talking with.

**Verification**:
PC generated random data and it will send it over to the website. To prove that it is the real website, PC tells the website to encrypt the data with its private key and send it back. PC decrypts it with public key and if data comes back the same, communication has been verified.

Asymmetric encryption is slow and should not be used for bulk data exchange like web browsing
Symmetric encryption should be used but you and the website do not have a shared key

## Asymmetric Encryption - Authenticity and Non-Repudiation

PC will generate a shared key and encrypt it with websites public key. Website will then decrypt it with their private key. You now have the same shared key on both sides of the link which can be used for symmetric encryption

# Site-to-Site VPN

- Use symmetric encryption algorithms such as DES, 3DES and AES to send encrypted traffic between locations over an untrusted network such as the Internet
- Traffic inside an office is often unencrypted as it is seen as a trusted network
- Site-to-Site VPN tunnels typically terminate on a firewall or router on both sides
- A preshared key can be used but certificates are better as they are more scalable

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
# Remote Access VPN

## Cisco AnyConnect Mobility Client

Cisco AnyConnect is a Remote Access VPN which uses the ASA firewall, terminates on the firewall
Uses TLS

## Split Tunneling

Corporate traffic goes over VPN tunnel to the corporate site
Public traffic will go directly to Internet, not through tunnel
Better performance

## Full Tunnel

All traffic go over VPN tunnel, but is redirected to Internet web server
Allows you to enforce security policy on staff

# Threat Defense Solutions

## Malware

Antimalware should be installed on host systems
Uses signatures and heuristics to detect malware
Users should be prevented from disabling software

## Malware, Phishing and Data Exfiltration

- Cisco Email Security Appliance scans links and attachments in incoming email for malware, phishing, and spam
- Cisco Web Security Appliance prevents users from accessing dangerous websites
- Policies can be implemented on ESA and WSA to prevent sensitive info from being sent out of the org
- Security awareness training should be implemented

## Reconnaissance and Social Engineering

- The best way to defend from passive reconnaissance and social engineering is through awareness training
- Deeper reconnaissance such as port and vulnerability scanners can be defended against using IPS
- It is not normal for a host to scan through a range of ports, an IPS can detect and drop the traffic

## DDoS

- IPS can detect DDoS attacks through anomaly-based inspection
- Advanced firewalls can offload incoming connection attempts from servers when traffic reaches a certain threshold
- Anti DDoS services monitor global Internet traffic to detect botnets and C&C servers
- Geographic dispersion of an organizations services can help mitigate DDoS attacks

## Spoofing, MITM and Reflection Attacks

- Unicast Reverse Path Forwarding (uRPF) verifies an source IP address is reachable through the same interface it was received on
- Attacker will not receive traffic back so they do not see the TCP sequence number. A target may be more vulnerable to attacks if it uses predictable TCP sequence numbers
- Advanced firewalls can also randomize TCP sequence number
- Secure Authentication
- Dynamic ARP inspection

## Password Attacks

- Firewalls and packet filters should be configured to prevent illegitimate users from having connectivity to login windows
- Password policies should be enforced
- Multifactor authentication
- Awareness training

## Buffer Overflow

Software should be patched and up to date to reject malformed data

## Packet Sniffers

Packet filters and firewalls should be used to ensure traffic paths are controlled
Traffic should be authenticated and encrypted if it passes over an untrusted network

## Penetration Tester

Uses same methods as a hacker
## References 



