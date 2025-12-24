2025-12-22 18:23
Flashcards:
Source: [[]]
Tags: [[]]


# Switches vs Hubs

Hubs and switches perform similar function. End hosts in a LAN plug into them with and ethernet cable which then allows the end hosts to communicate with each other

## Hubs - Half Duplex and Shared Collision Domain

- Hubs operate in half duplex mode. Attached hosts cannot send and receive at the same time, they can only do one or the other
- All hosts share the same collision domain - only one device can transmit at a time. If two hosts transmit at the same time a collision will occur. Hosts use Carrier-Sense Multiple Access with Collision Detection (CSMA/CD) to detect collisions

## Switches - Full Duplex and Separate Collision Domains

- Switches can operate in either full duplex or half duplex mode. In practice they always operate at full duplex. Attached host can send and receive data at the same time
- All hosts have their own collision domain, collision detection is not required

Hubs operate at Layer 1
Switches operate at Layer 2

### Switches Operate at Layer 2

When a frame is received, the switch will look at the source MAC address. The learned MAC address will be added to the switches MAC address table, which maps MAC address to ports

# Switch Operation

# Routers

- Routers know the path to get to different IP subnets on a network. They are required to send traffic from one subnet to another
- Routers operate at Layer 3 (They also operate at Layer 2 and 1, and will typically have awareness up to Layer 7)

## Switches vs Routers 

| Routers                                                                                                                                                | Switches                                                                                                                                  |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------- |
| - Layer 3 aware, routes between network<br>- Support many different interfaces (Ethernet, Serial, ISDN, ADSL)<br>- Do not broadcast traffic by default | - Layer 2 aware, switch traffic between LAN<br>- Typically only support Ethernet<br>- Have more ports than routers<br>- Broadcast traffic |

## Layer 3 Switches

Advanced switches are Layer 3 aware and can route traffic between subnets. Layer 3 switches will typically support only Ethernet interfaces and will have more ports than routers

# Other Cisco Devices

<span style="color:rgb(255, 0, 0)">A routers interface status is administratively down be default. The interface must be bought online to use</span>
## References
