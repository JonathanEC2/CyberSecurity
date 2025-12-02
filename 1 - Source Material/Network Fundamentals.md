
2025-10-28 14:01
Status:
Flashcards:
Source: [[]]
Tags: [[../2 - Tags/Networking|Networking]], [[../2 - Tags/OSI|OSI]]

## What is Networking?

- Networks are simply things connected.
- The Internet is one giant network that consists of many, many small networks within itself. 
- As previously stated, the Internet comprises many small networks all joined together.  These small networks are called private networks, whereas networks connecting these small networks are called public networks -- or the Internet
- An IP address can be used as a way of identifying a host on a network for a period of time
- A public address is used to identify the device on the Internet, whereas a private address is used to identify a device amongst other devices.
-  **MAC address** is a twelve-character hexadecimal number
- Ports are numbers assigned to uniquely identify a connection endpoint and to direct data to a specific service

## Intro to LAN

- **Star Topology** - devices are individually connected via a central networking device such as a switch or hub. This topology is the most commonly found today because of its reliability and scalability - despite the cost
- **Bus Topology** - relies upon a single connection known as a backbone cable. easier and more cost-efficient topologies to set up because of their expenses. little redundancy in place in case of failures. This disadvantage is because there is a single point of failure along the backbone cable.
- **Ring Topology** - may have to visit multiple devices first before reaching the intended device.  less prone to bottlenecks but a fault such as a cut cable, or broken device will result in the entire networking breaking.
- **Switches** are dedicated devices within a network that are designed to aggregate multiple other devices such as computers, printers, or any other networking-capable device using ethernet.
- It's a **router**'s job to connect networks and pass data between them.

| Type            | Purpose                                                                                                                                        | Explanation                                                                                                                                                                                                                                          | Example       |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| Network Address | This address identifies the start of the actual network and is used to identify a network's existence.                                         | For example, a device with the IP address of 192.168.1.100 will be on the network identified by 192.168.1.0                                                                                                                                          | 192.168.1.0   |
| Host Address    | An IP address here is used to identify a device on the subnet                                                                                  | For example, a device will have the network address of 192.168.1.1                                                                                                                                                                                   | 192.168.1.100 |
| Default Gateway | The default gateway address is a special address assigned to a device on the network that is capable of sending information to another network | Any data that needs to go to a device that isn't on the same network (i.e. isn't on 192.168.1.0) will be sent to this device. These devices can use any host address but usually use either the first or last host address in a network (.1 or .254) | 192.168.1.254 |

  

-  **Address Resolution Protocol** or ARP for short, is the technology that is responsible for allowing devices to identify themselves on a network. The ARP protocol allows a device to associate its MAC address with an IP address on the network. When an ARP request is sent, a message is broadcasted to every other device found on a network by the device, asking whether or not the device's MAC address matches the requested IP address. If the device does have the requested IP address, an ARP reply is returned to the initial device to acknowledge this. The initial device will now remember this and store it within its cache 

- IP addresses can be assigned either manually, by entering them physically into a device, or automatically and most commonly by using a DHCP (Dynamic Host Configuration Protocol) server. When a device connects to a network, if it has not already been manually assigned an IP address, it sends out a request (DHCP Discover) to see if any DHCP servers are on the network. The DHCP server then replies with an IP address the device could use (DHCP Offer). The device then sends a reply confirming it wants the offered IP Address (DHCP Request), and then lastly, the DHCP server sends a reply acknowledging this has been completed, and the device can start using the IP Address (DHCP ACK).
    
## OSI Model

- **Layer 7** -  the application layer is the layer in which protocols and rules are in place to determine how the user should interact with data sent or received. Provides a friendly, Graphical User Interface (GUI) for users to interact with data sent or received.
- **Layer 6** - The presentation layer acts as a translator for data to and from the application layer. Security features such as data encryption occur at this layer.
- **Layer 5** - the session layer (layer 5) will begin to create a connection to the other computer that the data is destined for. The session layer (layer 5) synchronizes the two computers to ensure that they are on the same page before data is sent and received. Sends data in chunks
- **Layer 4** -  Transmission Control Protocol (TCP). This protocol is designed with reliability and guarantee in mind.  TCP incorporates error checking into its design. Any data that gets sent via UDP is sent to the computer whether it gets there or not. There is no synchronization between the two devices or guarantee. <span style="color:rgb(255, 0, 0)">Segment</span>
- **Layer 3** - The network layer is where the magic of routing & re-assembly of data takes place. Routing simply determines the most optimal path in which these chunks of data should be sent. OSPF (Open Shortest Path First) and RIP (Routing Information Protocol) determine exactly what is the "optimal" path that data should take to reach a device. <span style="color:rgb(255, 0, 0)">Packet</span>
- **Layer 2** - The data link layer focuses on the physical addressing of the transmission. It receives a packet from the network layer (including the IP address for the remote computer) and adds in the physical MAC (Media Access Control) address of the receiving endpoint. <span style="color:rgb(255, 0, 0)">Frame</span>
- **Layer 1** - physical components of the hardware used in networking  


## Packets and Frames

Packets and frames are small pieces of data that, when forming together, make a larger piece of information or message. think of this as putting an envelope within an envelope and sending it away. The first envelope will be the packet that you mail, but once it is opened, the envelope within still exists and contains data (this is a frame). This process is called encapsulation.

  
The TCP/IP protocol consists of four layers and is arguably just a summarized version of the OSI model. These layers are:

- Application
- Transport
- Internet
- Network Interface / Link

## Extending Your Network

Port forwarding is an essential component in connecting applications and services to the Internet. Without port forwarding, applications and services such as web servers are only available to devices within the same direct network.

A firewall is a device within a network responsible for determining what traffic is allowed to enter and exit.

- Where is the traffic coming from? 
- Where is the traffic going? 
- What port is the traffic for? 
- What protocol is the traffic using? 


| Firewall Category | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Stateful          | This type of firewall uses the entire information from a connection; rather than inspecting an individual packet, this firewall determines the behavior of a device based on the entire connection.<br><br>This firewall type consumes many resources in comparison to stateless firewalls as the decision-making is dynamic. For example, a firewall could allow the first parts of a TCP handshake that would later fail.<br><br>If a connection from a host is bad, it will block the entire device.                                                                                                                                         |
| Stateless         | This firewall type uses a static set of rules to determine whether or not individual packets are acceptable or not. For example, a device sending a bad packet will not necessarily mean that the entire device is then blocked.<br><br>Whilst these firewalls use much fewer resources than alternatives, they are much dumber. For example, these firewalls are only effective as the rules that are defined within them. If a rule is not exactly matched, it is effectively useless.<br><br>However, these firewalls are great when receiving large amounts of traffic from a set of hosts (such as a Distributed Denial-of-Service attack) |

  
Routing is the label given to the process of data traveling across networks. Routing involves creating a path between networks so that this data can be successfully delivered. Routers operate at Layer 3 of the OSI model.

Switches can operate at both layer 2 and layer 3 of the OSI model. However, these are exclusive in the sense that Layer 2 switches cannot operate at layer 3. Layer 2 switches will forward frames onto the connected devices using their MAC address. Layer 3 switches will send frames to devices (as layer 2 does) and route packets to other devices using the IP protocol. 

A technology called VLAN (Virtual Local Area Network) allows specific devices within a network to be virtually split up. [[../../5. Security Engineer/3. Network and System Security#Need for Secure Segmentation]]


## References
  

