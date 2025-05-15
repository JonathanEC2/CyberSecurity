
# Very Basic Introduction to Networking 

Switch allows connectivity to a LAN

A wireless access point is a device that enables wireless network connectivity for devices, acting as a bridge between a wired network and a wireless device

LAN is a network that connects devices in the same area

Routers make advanced routing decisions to route traffic between different areas of your network

Wide Area Networks spans cross multiple areas

Network Characteristics
- Topology
- Speed
- Cost
- Security
- Availability
- Scalability
- Reliability

# The OSI Reference Model Overview

The Open System Interconnect model is a standard of the International Organization for Standardization. Its a general purpose framework that standardizes how computer communicate with each other over a network. A layer serves the layer above it and it is serves by a layer below it

Sender builds packet from the top and works its way down the model. They layer above is encapsulated by the layer below. Layers 5-7 are known as the upper layers, more important for app developers than network engineers

The receiver of the information will process the information backwards, starting from layer 1 upward (decapsulation):

- Comes in on Physical layer
- Checks Layer 2 header to check destination MAC address, will check that this packet is for it
- Checks Layer 3 for destination IP address, will check that this packet is for it
- Checks Layer 4 header, checks what port info was sent over

# The TCP/IP Stack

A protocol controls how communication should behave

Main protocol used stack used in computer operations today. It is used to transfer data in production networks

- Application - represents data users, encodes and controls the dialog
- Transport - supports communication across different devises across a network
- Internet - provides logical addressing and determines best path through the network
- Link - controls the hardware devices and media that make up the network

## Host Communication Terminology

When two hosts talk to each other, they exchange Protocol Data Units (PDUs). The PDU is the entire communication starting at Layer 7 all the way down to Layer 1

Application - Data
Transport - Segment
Internet - Packet
Link - Frame
# The Upper OSI Layers

## Layer 7 - Application

- Provides network services to the applications of the user. It does not provide a service to any other OSI layer
- Establishes availability of intended communication partner
- Establishes agreement of procedures for error recovery and control of data integrity

## Layer 6 - Presentation

Ensures information that is sent at the application layer is readable by the application of another system. The presentation layer can translate among multiple data formats using a common format

## Layer 5 - Session

Establishes, manages, and terminates sessions between communicating hosts. Session layer synchronizes dialog between the presentation layers of the two hosts and manages their data exchange. 

It also offers data transfer, Class of Service (CoS), which is similar to efficient data transfer, and  reporting of upper layer problems.

# The Lower OSI Layers

## Layer 4 - Transport

Determines whether TCP or UDP is used and what port number

Defines services to segment, transfer, and reassemble the data for individual communications between the end devices. It breaks down large files into smaller segments that are less likely to incur transmission problems
## Layer 3 - Network

Source and destination IP address. Routers operate here

Provides connectivity and path selection between two host systems that may be located on two geographically separate networks. Manages the connectivity of hosts by providing logical addressing
## Layer 2 - Data Link

Source and destination Layer 2 address. Switches operate here

The data link layer defines how data is formatted for transmission and how access to physical media is controlled. It typically includes error detection and correction to ensure a reliable delivery of data
## Layer 1 - Physical

Physical components of the network

Enable bit transmission between devices. It defines specifications needed for activating, maintaining, and deactivating the physical link between devices. This includes voltage, physical data rates, max transmission distances, physical connectors, etc. 