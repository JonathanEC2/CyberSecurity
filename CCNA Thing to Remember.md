ISP network is only configured on the external facing router
Priority is set on the interface level
Set IP address on subinterface 
RoaS uses trunk ports on switch
Configure IP address on port channel on a Layer 3 switch
DHCP helper address points directly to DHCP server
Access lists have an implicit deny rule, must explicitly permitted traffic. 
For PAT translation with one address, you don't configure a pool and point to interface

`transport input ssh (telnet not added)`

`crypto key generate rsa`

 Terraform uses HashiCorp Configuration Language or JSON
 
The . character indicates that either the local device does not have a path to the destination or that the destination does not have a path back to the local device. The U character, on the other hand, indicates that a device somewhere between the ping source and destination devices does not a have a path to the destination.

Ping verifies TWO WAY connectivity. All devices need routes to the other

Encapsulation protocols operate at the Data Link layer of the Open Systems Interconnection (OSI) networking model. There are two primary encapsulation methods used on Cisco Serial interfaces: High-level Data Link Control (HDLC) and PPP. HDLC is the default protocol on Cisco serial links.

A stub host, or OSPF stub network, is typically a network in which only a single router resides. Because none of the routers have formed adjacencies, each OSPF router in this topology is currently a stub.

By default, the Hello timer is set to 10 seconds on Ethernet, point-to-point, and broadcast links and is set to 30 seconds on NBMA links.

- Broadcast interfaces are typically found on Ethernet networks. In this scenario, the OSPF routers are all connected by using FastEthernet interfaces. Broadcast interfaces can find OSPF neighbors automatically. Router elections for DR and BDR are performed on broadcast networks.
- An NBMA network does not support broadcasts but does support multiple devices being connected to the network. Router elections for DR and BDR are performed on NBMA networks.
- Point-to-point networks have a direct connection between two endpoints. Point-to-point interfaces are typically found on High-Level Data Link Control (HDLC) HDLC or Point-to-Point Protocol (PPP) serial interfaces. Router elections for DR and BDR are not performed on point-to-point networks.
- Point-to-multipoint networks involve multiple devices connecting to a shared single endpoint. These networks can be either broadcast or NBMA. Router elections for DR and BDR are not performed on point-to-multipoint networks.

The Cisco IOS traceroute command works by sending User Datagram Protocol (UDP) traffic with a Time To Live (TTL) value of 1 to a port number that is unlikely to be open and listening at the remote host. The low TTL causes the device at each hop, or router, along the path to the destination to reply to the UDP traffic with an Internet Control Message Protocol (ICMP) Time Exceeded Message (TEM), which means that the device at the hop received and discarded the UDP traffic.

The AAA Override feature on a Cisco wireless LAN controller (WLC) can be used to configure virtual local area network (VLAN) tagging, Quality of Service (QoS), and access control lists (ACLs) to individual clients based on Remote Authentication Dial-In User Service (RADIUS) attributes. When