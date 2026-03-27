2025-12-22 16:49
Flashcards:
Source: [[]]
Tags: [[]]

# Ethernet Connection Media

OSI Layer 1 conveys the bit stream through the network at the electrical and mechanical level

## Layer 1 Connection Types for Ethernet UTP

- Ethernet LAN cabled can be transmitted over twisted copper pair cables, fiber cables, or wireless
- Copper UTP (Unshielded Twisted Pair) cables are commonly used to connect desktops to switches
- Connector type is RJ-45 and maximum length is 100 meters

### Straight-Through vs Crossover UTP Cable

Wires in an RJ-45 connector can be either straight through or crossover

- Straight through cables are often used to connect an end device such as a PC or router to a switch
- Crossover cables are used to connect devices together directly, most commonly two devices of the same type (two PCs or two switches to each other)
- Modern switches support Auto MDI-X where the receive and transmit signals are reconfigured automatically (you can use a straight through cable to connect two switches and be fine)

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
