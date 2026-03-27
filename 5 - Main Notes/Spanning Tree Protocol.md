2026-03-24 18:52
Tags: [[]]



## Spanning Tree Protocol (STP)

- Spanning Tree blocks ports to prevent loops. This means the access layer switches can only use half of their physically cabled uplink bandwidth
- Spanning tree automated failover as well as performing loop prevention
- Legacy Spanning Tree can take up to 50 seconds to converge

## Layer 2 Loops

- Layer 2 Ethernet header does not have a TTL field to stop the looping traffic

# How Spanning Tree Works

- Spanning Tree is enabled by default on all vendors switches
- Switches send Bridge Protocol Data Units out all ports when they come online. These are used to detect other switches and potential loops
- The switch will not forward traffic out any port until it is certain it is loop free

## The Bridge ID

- The BPDU contains the switch's Bridge ID which uniquely identifies the switch on the LAN
- The Bridge ID is comprised of the switch's MAC address and and administrators defined Bridge Priority value. The Bride Priority can be from 0 - 65535 with 32768 being default

## The Root Bridge

The Root Bridge is elected based on the switches' Bridge ID values. The switch with the lowest Bridge Priority is preferred.
In the case of a tie, the switch with the lowest MAC address will win

## Spanning Tree Path Cost

- Spanning Tree is built with the Root Bridge at the top. All switches forward traffic on the lowest cost path to the Root Bridge
- The cumulative STP cost across all links to reach the Root Bridge is chosen as the Root Path
- A Root Path Cost is a switches cumulative cost for a specific path to reach the Root Bridge

## Root Ports

- Each switch's exit interface on the lowest cost path to the Root Bride is selected as its Root Port
- Each switch only has one Root Port in the Spanning Tree
- - If a switch has multiple equal cost paths to the Root Bridge, it will select the neighbor switch with the lowest Bridge ID
- If a switch has multiple equal cost paths via the same neighbor switch towards the Root Bridge, it will select the port with the lowest Port ID (f0/1) on the neighbor switch

## Designated Ports

- Ports on the neighbor switch opposite the Root Port are Designated Ports
- Root Ports point towards the Root Bridge, Designated Ports point away from it
- All ports on the Root Bridge are always Designated Ports

## Blocked Ports

- Spanning Tree only blocks ports on one side of the blocked link
- BPDUs continue to be sent over the link from the Designated Port (but not from the Blocked Port)
- <span style="color:rgb(255, 0, 0)">Alternate ports receive more useful BDPUs from a designated port on another switch. An alternate port guarantees a path to the Root Bridge should the current Root Port become unavailable</span>
- <span style="color:rgb(255, 0, 0)">A backup port receives more useful BDPUs from the same switch. Only guarantees redundant access to a particular network segment but not necessarily an alternate path to the Root Bridge </span>
- If a Blocked Port stops receiving better BPDUs it will unblock and transition to being a Designated (Forwarding) Port
- PORTS ON ROOT BRIDGE ARE NEVER BLOCKED

# Spanning Tree Versions

IEEE Open Standards:
- 802.1D *1998* (STP): The original Spanning Tree implementation. Uses one spanning tree for all VLANs in the LAN
- 802.1w Rapid STP (RSTP): Significantly improved convergence time. Use one Spanning tree for all VLANs in the LAN
- 802.1s Multiple STP (MSTP): Enables **grouping** and mapping into different VLANs into different spanning tree instances for load balancing

 Cisco Versions: 
- Per VLAN Spanning Tree Plus (PVST+): Cisco enhancement to 802.1D. Uses a separate Spanning Tree instance for every VLAN. This is the default on most Cisco switches.
- Rapid Per VLAN Spanning Tree Plus (RPVST+): Cisco enhancement to 802.1w RSTP. Significantly improved convergence time over PVST+. Uses separate Spanning Tree instance for every VLAN

```IOS
spannning-tree mode ?
show spanning-tree summary
```

## Port Roles and States

| 802.1D Port Role                                           | Port State                                                    |
| ---------------------------------------------------------- | ------------------------------------------------------------- |
| Root                                                       | Forwarding                                                    |
| Designated                                                 | Forwarding                                                    |
| <span style="color:rgb(0, 176, 240)">Non-Designated</span> | <span style="color:rgb(0, 176, 240)">Blocking</span>          |
| Disabled                                                   |                                                               |
| In transition                                              | <span style="color:rgb(255, 0, 0)">Listening</span>, Learning |

| RSTP Port Role                                                                                         | Port State                                             |
| ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------ |
| Root                                                                                                   | Forwarding                                             |
| Designated                                                                                             | Forwarding                                             |
| <span style="color:rgb(0, 176, 240)">Alternate</span>/<span style="color:rgb(255, 0, 0)">Backup</span> | <span style="color:rgb(0, 176, 240)">Discarding</span> |
| DIsabled                                                                                               | <span style="color:rgb(0, 176, 240)">Discarding</span> |
| In transition                                                                                          | Learning                                               |

Unidirectional Link Detection (UDLD)
Enabling Portfast default will only affect access ports
## References
