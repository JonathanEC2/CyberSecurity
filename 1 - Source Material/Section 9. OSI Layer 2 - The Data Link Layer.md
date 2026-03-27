2025-12-14 21:56
Flashcards:
Source: [[]]
Tags: [[]]

# Local Area Network Layer 2 - Ethernet

Frames are encoded and decoded into bits at Layer 2
Error detection and correction for the Physical Layer can be provided here

## The Media Access Control MAC Address

- Ethernet uses a 48-bit hexadecimal MAC address
- The first 24 bits in the OUI (Organizationally Unique Identifier) which uniquely identifies the manufacturer of the Ethernet port. It is assigned by the IEEE. The last 24 bits are vendor assigned. 
- The burned in MAC address on every NIC port in the world is globally unique

The EtherType field is used to indicate the protocol being encapsulated in the payload. It uniquely identifies upper layer protocols
The Ethernet frame check sequence (FCS) field contains a 4-byte cyclic redundancy check (CRC) value.

The Content Addressable Memory (CAM) table is used by a switch to discover the relationship between the Open Systems Interconnection (OSI) Layer 2 address of a device and the physical port used to reach the device. Switches make forwarding decisions based on the destination MAC address
## References
