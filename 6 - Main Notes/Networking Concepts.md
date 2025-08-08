---
sr-due: 2025-05-12
sr-interval: 4
sr-ease: 270
---

#review

[[../2 - Tags/Networking|Networking]]
# Network Concepts

## OSI model / TCP IP Model

| Layer        | Description                                                                                                                                                                                        |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Application  | Works almost exclusively with applications, providing an interface for them to use to transmit data. **(SNMP, HTTP, FTP)**                                                                         |
| Presentation | Translates the data into a standardized format, as well as handling any encryption, compression, or other transformations to the data. **(ASCII, PNG)**                                            |
| Session      | Establishes a connection between devices **(SYN/ACK)**                                                                                                                                             |
| Transport    | Sets up direct communication between connected devices **(TCP,UDP)**                                                                                                                               |
| Network      | Responsible for routing data, and locating the destination of your request. Logical addressing **(IP, Routers)**                                                                                   |
| Data Link    | Communication between locally connected devices. checks the received information to make sure that it hasn't been corrupted during transmission. Physical addressing **(MAC addresses, Switches)** |
| Physical     | The hardware of the computer; converts the binary data of the transmission into signals and transmits them across the network **(RJ45)**                                                           |

## Telnet
The TELNET (Teletype Network) protocol is a network protocol for remote terminal connection. In simpler words, telnet, a TELNET client, allows you to connect to and communicate with a remote system and issue text commands