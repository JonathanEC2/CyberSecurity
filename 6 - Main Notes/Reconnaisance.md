#reconnaisance
# FTP
- Explicit FTPS;; enables secure FTP over TCP port 20 and 21. ++explicit FTPS configuration requires the FTP client to request a secure connection from the FTPS server
- Implicit FTPS;; will not negotiate security with FTP client, the client must already be configured to operate with correct encryption method. Operates on port 989 and 990
- SFTP uses SSH over port 22

# HTTP
- Setting HttpOnly flag in the Set-Cookie field mitigates cookies being stolen which mitigates XSS attacks

# DNS
### Tools
- Bluto;; <span style="color:rgb(255, 0, 0)">Python</span>-based; uses<span style="color:rgb(255, 0, 0)"> Alexa Top 1 million</span> subdomain lists during an attempt to brute force sub domains of a target. Can query MX, NS, and AXFR query to discover subdomains
- InstaRecon uses  <span style="color:rgb(255, 0, 0)">Shodan</span> to query open ports, can perform basic DNS enum
- Dnsenum <span style="color:rgb(255, 0, 0)">Perl</span> script used to enum target domain
- SubBrute recursively <span style="color:rgb(255, 0, 0)">crawls</span> enum DNS records similar to a search engine spider crawling a website
### Attacks

Domain hijacking;; <span style="color:rgb(255, 0, 0)">name servers</span> that are resolved to a targets top-level domain are modified, redirecting requests for those domains to a malicious server
DNS hijacking;; <span style="color:rgb(255, 0, 0)">malware</span> is used to hijack a DNS service and is placed under the control of the attacker
DNS flooding;; Dos attack, overwhelms DNS server with traffic
DNS spoofing/cache poising;; inserts malicious name resolution to IP data in a DNS server. When target queries DNS server, reply directs target to a different website
DNS amplification/reflection;; attackers sends a flood of DNS queries from their own servers, but the queries contain spoofed source addresses that are sent to the address of target
# SMB 
SMB;; port 445 - enables file and printer sharing without the need for NETnjwhoisBIOS broadcasting

# SNMP
SNMP;; port 161 - SNMP3 is the only version that supports authentication and encryption

# SMTP
SMTP;; port 25 - EHLO initiates SMTP conversation with ESMTP, HELO for SMTP
# LDAP
### Tools
Luma Python based LDAP browser
Jxplorer;; Java based LDAP browser
Gawor's Java based LDAP browser; speed, stability, features
Coral Directory - Windows app, similar to JX and Gawor's features 
# Nmap

## Commands

-PP;; timestanp
-PE;; echo
-PM;; mask
-PO;; IP protocol scan
 -D;; performs a decoy scan

enip-info shows device type, vendor id, serial number, 
smb-os-discovery OS
s7-info shows basic hardware, system name, copyright, module
pc-worx-info shows firmware, plc type, and model number


TCP Scanning
- If port is open, target host will send a SYN/ACK to the zombie. The zombie will reply with an ACK, incrementing the IPIDS by 1. When the attacker sends another SYN/ACK packet to the zombie, the zombie will reply incrementing the IPID by 2. 
- If host is closed IPID will not increment again

# hping

creates custom packets for network testing

hping -0/,, --rawip specifies raw IP packet
hping -1/,, --icmp specifies icmp
hping -2/,, --udp specifies udp
hping -c,, the count of the packets sent to the target machine
No specification for TCP

Windows doesn't respond to ICMP echo requests directed at broadcast addresses. Apple OS and Linux will respond unless firewall rules prevent response
# Other 
ZoomInfo,,  provides tools to assists sales reps with searching target markets, planning territories, and generating new business leads

Diversion theft,,  when an attacker tricks a delivery person into delivering a package to the wrong location or wrong individual

![[Pasted image 20240814113540.png]]