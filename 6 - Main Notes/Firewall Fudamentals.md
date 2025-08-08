#security_solutions

[[../2 - Tags/Security Solutions|Security Solutions]]
# Firewall Fundamentals

A firewall is designed to inspect a network's or digital device’s incoming and outgoing traffic.  The goal is to not let any unauthorized traffic enter a system or a network. . You instruct the firewall by giving it rules to check against all the traffic. It allows or denies rules based on the rules you give it. 

## Types of Firewalls

Different types of firewalls work at different OSI model layers

#### Stateless Firewall

Operates at layer 3 and 4 of the OSI model and works solely by filtering data based on previous rules without taking note of the state of previous connections. These firewalls process packets quickly but cannot apply complex policies to the data based on its relationship with the previous connection. 

#### Stateful Firewall

Operate at layer 3 and layer 4 of the OSI model. Filters packets by predetermined rules as and keeps track of previous connections and stores them in a state table. Stateful firewalls take note of the connections for which they deny a few packets, and based upon this information, they deny all the subsequent packets coming from the same source.

#### Proxy Firewall

 Proxy firewalls, or application-level gateways, act as intermediaries between the private network and the Internet and operate on the OSI model’s layer 7. They inspect content of all packets as well. A user request is forwarded by this proxy after inspection and masks them with their own IP address to provide anonymity for the internal IP addresses.

#### Next-Generation Firewall (NGFW)

Most advanced type of firewall that operates from layer 3 to layer 7 of the OSI model. Offers deep packet inspection and other functionalities that enhance the security of incoming and outgoing traffic. It has an IPS that blocks malicious activities in real time. Offers heuristic analysis by analyzing the patterns of attacks and blocking them before reaching the network.

## Rules in Firewalls

**Source address**: The machine’s IP address that would originate the traffic.
**Destination address**: The machine’s IP address that would receive the data.
**Port**: The port number for the traffic.
**Protocol**: The protocol that would be used during the communication.
**Action**: This defines the action that would be taken upon identifying any traffic of this particular nature.
**Direction**: This field defines the rule’s applicability to incoming or outgoing traffic.

#### Types of Actions

Allow indicates that certain traffic is allowed
Deny means that the traffic defined inside the rule would be blocked and not permitted
Forward redirects traffic to a different network segment

#### Directionality of Rules

Inbound: applied to incoming traffic only
Outbound: outgoing traffic only
Forward:  forwards specific traffic inside the network

## Windows Defender Firewall

This firewall contains all the basic functionality for creating, allowing, or denying specific programs or creating customized rules.

#### Network Profiles

 Windows firewall determines your current network based on Network Location Awareness (NLA) and applies that profile firewall settings for you.
 
**Private networks**: This includes the firewall configurations to apply when connected to our home network.
**Guest or public networks**: This includes the firewall configurations to apply when connected to a public or untrusted network like coffee shops, restaurants, or similar

#### Custom Rules

Windows Defender Firewall also allows you to create custom rules for your network to allow/disallow specific traffic as needed.
## Linux iptables Firewall

#### Netfilter

Netfilter is the framework inside the Linux OS with core firewall functionalities, including packet filtering, NAT, and connection tracking. This is the foundation for many firewall utilities in Linux. Some firewalls that utilize this framework are:

**iptables**: This is the most widely used utility in many Linux distributions.
**nftables**: It is a successor to the “iptables” utility, with enhanced packet filtering and NAT capabilities.
**firewalld**: This utility also operates on the Netfilter framework and has predefined rule sets.

#### ufw

<span style="color:rgb(255, 192, 0)">ufw status</span>
<span style="color:rgb(255, 192, 0)">ufw allow to</span> or <span style="color:rgb(255, 192, 0)">from</span>