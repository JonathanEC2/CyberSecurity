---
sr-due: 2025-06-11
sr-interval: 34
sr-ease: 223
---
[[../2 - Tags/Networking|Networking]]

#review 
## TLS

Cryptographic protocol operating at layer 4. Allows secure communication between a client and a server over and insecure network. 

#### Technical Background 

1. First step for every server (or client) needs to identify itself to get a signed TLS certificate (Generally, the server administrator creates a Certificate Signing Request (CSR) and submits it to a Certificate Authority (CA))
2. Once the signed certificate is received, it can be used to identify the server (or client) to others, who can confirm the validity of the signature. For a host to confirm the validity of a signed certificate, the certificates of the signing authorities need to be installed on the host.

## HTTPS

Steps before a web browser can request a web page over **HTTP**:
1. Establish a three-way handshake with the target server
2. Communicate using the HTTP protocol; for example, issue HTTP requests, such as GET / HTTP/1.1

Requesting a page over **HTTPS** will require the following three steps (after resolving the domain name):
1. Establish a TCP three-way handshake with the target server
2. Establish a TLS session
3. Communicate using the HTTP protocol; for example, issue HTTP requests, such as GET / HTTP/1.1

  
## SMTPS, POP3S, and IMAPS

Adding TLS to SMTP, POP3, and IMAP is no different than adding TLS to HTTP. Traffic is no longer sent in cleartext

| Protocol | Default Port Number |
| -------- | ------------------- |
| HTTPS;;  | 443                 |
| SMTPS;;  | 465 and 587         |
| POP3S;;  | 995                 |
| IMAPS;;  | 993                 |

## SSH 

OpenSSH benefits:
- Secure authentication: supports password based, public key, and two factor authentication 
- Confidentiality: provides end to end encryption
- Integrity
- Tunneling: can create a tunnel to route to other protocol
- X11 forwarding

The argument <span style="color:rgb(0, 176, 240)">-X</span> is required to support running graphical interfaces, for example, ssh 192.168.124.148 -X
## VPN

creates a secure, encrypted connection over the internet and masks IP by routing data through a remote server