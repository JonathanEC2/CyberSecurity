2026-03-25 21:50
Tags: [[]]

# Layer 4 - Transport

Transport layer is responsible for end to end error recovery and flow control. **Flow control** is the process of adjusting the flow of data from the sender to ensure receiving host can handle it all.

Layer 4 destination port number is used to identify the upper layer protocol. The combination of source and destination port numbers are used to track sessions

## TCP Header
 
![[attachments/Pasted image 20260325215400.png]]

## UDP Header

![[attachments/Pasted image 20260325215416.png]]

# Layer 3 - Network

Responsible for routing packets to their destination and QoS
Internet Protocol is a connectionless protocol with no acknowledgement at Layer 3
ICMP and IPsec also operate at Layer 3

## IP Header

![[attachments/Pasted image 20260325215719.png]]

## Subnet Mask

Defines the host portion and the network portion of an address

# Layer 2 - Ethernet

Frames are encoded and decoded into bits at Layer 2. Error detection and correction are performed at this layer as well

The Content Addressable Memory table is used by a switch to discover the relationship between the OSI Layer 2 address of a device and the physical port used to reach the device. Switches make forwarding decisions based on destination MAC address
## MAC Address

- Uses a 48-bit (8 byte) hexadecimal MAC address
- First 24 bits are the OUI which uniquely identifies the manufacturer of the Ethernet port. It is assigned by the IEEE
- The last 24 bits are vendor assigned

## Ethernet Header 

![Ethernet Frames (7.1) > Ethernet Switching | Cisco Press](https://www.ciscopress.com/content/images/chap7_9780136633662/elementLinks/07fig04_alt.jpg)

- **Preamble** helps the sender and the receiver to synchronize
- **Ethertype** field in the Ethernet header is used to specify what is encapsulated inside the data of the Ethernet frame.
- **Frame Check Sequence** is a cyclical redundancy check which is used to check for the integrity of the frame

# Layer 1 - Physical Layer

Layer 1 conveys the bitstream through the network at the electrical and mechanical level

## Connection Types

- Ethernet LAN cabled can be transmitted over twisted copper pair cables, fiber cables, or wireless
- Copper UTP (Unshielded Twisted Pair) cables are commonly used to connect desktops to switches
- Connector type is RJ-45 and maximum length is 100 meters

### Straight-Through vs Crossover UTP Cable

- Straight through cables are often used to connect an end device such as a PC or router to a switch
- Crossover cables are used to connect devices together directly, most commonly two devices of the same type (two PCs or two switches to each other)
- Auto MDI-X reconfigure the receive and transmit signals automatically (you can use a straight through cable to connect two switches and be fine)

## Fiber Cables 

## Fiber Cables

- Fiber cables support longer distances or higher bandwidth requirements
- Plugged into a transceiver that then plugs into a router or switch

### Single Mode vs Multi Mode

- Single mode supports higher bandwidth and longer distances but is more expensive
- Multi mode only supports a few hundred meters 
- PoE (power over ethernet) switch sends power over Ethernet, don't need a separate power supply for IP phone



- **1000BaseZX**: A standard for long-reach transmission over single-mode fiber, extending up to 70-100 km.
- **1000BaseCX**: An early standard for short-distance transmission using balanced shielded copper cabling.
- **1000BaseLX**: A standard for long-wavelength transmission over single-mode and multi-mode fiber, commonly used in campuses.
- **1000BaseSX**: A standard for short-wavelength transmission over multi-mode fiber, typically used for backbone connections within buildings.

## References
