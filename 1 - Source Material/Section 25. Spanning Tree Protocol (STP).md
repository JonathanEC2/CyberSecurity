
2026-02-18 20:45
Tags: [[]]

# Layer 3 Path Selection and Loop Prevention Review

- Layer 3 routing and HSRP control the path selection and provide automatic failover for Layer 3 
- Dynamic Routing Protocols have built in loop prevention mechanisms and TTL acts as a final failsafe

# Why We Have Spanning Tree Protocol

## Layer 2 Loops

- Layer 2 Ethernet header does not have a TTL field to stop the looping traffic
- This will cause a broadcast storm of broadcast traffic between switches. The network will crash because the amount of looping broadcast traffic will quickly overwhelm the switch's CPU and bandwidth
- Broadcast storms are disastrous for the LAN and must be avoided at all costs
- The Spanning Tree Protocol is used to prevent Layer 3 loops. It does this by detecting potential loop and blocking ports to prevent them

## Spanning Tree Protocol (STP)

- Spanning Tree blocks ports to prevent loops. This means the access layer switches can only use half of their physically cabled uplink bandwidth
- Spanning tree automated failover as well as performing loop prevention
- Legacy Spanning Tree can take up to  50 seconds to converge

# Spanning Tree Terminology - The Bridge 

- A bridge was used in environments with hubs to separate large collision domains into smaller ones. Bridges only had two ports
- A switch is a multi-port bridge
- Spanning Tree was invented back when bridges were in use so it uses that terminology ('Root Bridge' and 'Bridge Protocol Data Units')

# How Spanning Tree Works

- Spanning Tree is enabled by default on all vendors switches
- Switches send Bridge Protocol Data Units out all ports when they come online. These are used to detect other switches and potential loops
- The switch will not forward traffic out any port until it is certain it is loop free

## Spanning Tree Port States

- When the port first comes online it will be blocking (not forwarding) traffic
- Spanning Tree will detect if the port forms a potential loop. If there is no loop the port will transition to Forwarding. This process can take up to 50 seconds

## The Bridge ID

The BPDU contains the switch's Bridge ID which uniquely identifies the switch on the LAN
The Bridge ID is comprised of the switch's MAC address and and administrators defined Bridge Priority value. The Bride Priority can be from 0 - 65535 with 32768 being default

## The Root Bridge

A Root Bridge is elected based on the switches' Bridge ID values. The switch with the lowest Bridge Priority value id preferred. In the case of a tie, the switch with the lowest MAC address will win
The switches build a loop free forwarding path Tree leading back to the Root Bridge

## Spanning Tree Cost

![[../attachments/Spanning Tree Cost.png]]


- Short-Mode (default): the original standard, a 16-bit value. Reference bandwidth is 20 Gbps, not granular enough for todays high bandwidth networks
- Long-Mode: 32-bit value. More granular, reference bandwidth is 20 Tbps
- <span style="color:rgb(255, 0, 0)">Ensure you enable long mode on all of you switches</span>

`show spanning tree pathcost method`

## Spanning Tree Path Cost

- The spanning tree is built with the Root Bridge at the top. All switches forward traffic on their best (lowest cost) path to the Root Bridge. Higher cost paths (which could potentially cause loops) are blocked
- The cumulative STP cost across all links to reach the Root Bridge is chosen as the switches Root Path
- A Root Path Cost is a switch's cumulative cost for a specific path to reach the Root Bridge

## Root Ports

- Each switch's exit interface on the lowest cost path to the Root Bride is selected as its Root Port
- Each switch only has one Root Port in the Spanning Tree

## Load Balancing

- A spanning tree instance does not do load balancing
- If a switch has multiple equal cost paths to the Root Bridge, it will select the neighbor switch with the lowest Bridge ID
- If a switch has multiple equal cost paths via the same neighbor switch towards the Root Bridge, it will select the port with the lowest Port ID (f0/1) on the neighbor switch

## Designated Ports

- Ports on the neighbor switch opposite the Root Port are Designated Ports
- Root Ports point towards the Root Bridge, Designated Ports point away from it
- All ports on the Root Bridge are always Designated Ports

- Root ports and their opposing Designated Ports are the most direct path to and from the Root Bridge and transition to a forwarding state

## Other Links

- On the remaining links, the switches determine which of them has the least cost path to the root. If they have equal cost paths then the Bridge ID is used as a tie breaker. These ports will be used as Designated Ports
- Any ports that have not been selected as a Root or Designated Port pair would potentially form a loop. These are selected as Blocking Ports

## Blocked Ports

- Spanning Tree only blocks ports on one side of the blocked link
- BPDUs continue to be sent over the link from the Designated Port (but not from the Blocked Port)
- Other traffic cannot use the link

![[../attachments/Pasted image 20260220171440.png]]

If a Blocked Port stops receiving better BPDUs it will unblock and transition to being a Designated (Forwarding) Port

![[../attachments/Pasted image 20260220171803.png]]

## Root Designated and Blocking Ports

Easy way to figure out which ports are Root, Designated, and Blocking:

1. Determine the Root Bridge first (best Bridge ID)
2. All ports on the Root Bridge are Designated Ports
3. Determine the Root Ports on other switches (lowest cost Root Bridge)
4. The ports on the other side of those links are Designated Ports
5. On the links which are left, one will be Blocking
6. Determine the Blocking Port (highest cost path to the Root Bridge or highest Bridge ID)
7. The ports on the other side of those links are Designated Ports

# Spanning Tree Versions

IEEE Open Standards:
- 802.1D *1998* (STP): The original Spanning Tree implementation. Uses one spanning tree for all VLANs in the LAN
- 802.1w Rapid STP (RSTP): Significantly improved convergence time. Use one Spanning tree for all VLANs in the LAN
- 802.1s Multiple STP (MSTP): Enables **grouping** and mapping into different VLANs into different spanning tree instances for load balancing

 Cisco Versions: 
- Per VLAN Spanning Tree Plus (PVST+): Cisco enhancement to 802.1D. Uses a separate Spanning Tree instance for every VLAN. This is the default on most Cisco switches.
- Rapid Per VLAN Spanning Tree Plus (RPVST+): Cisco enhancement to 802.1w RSTP. Significantly improved convergence time over PVST+. Uses separate Spanning Tree instance for every VLAN

Cisco versions do not support grouping multiple VLANs in the same instance

## MSTP, PVSTP+, and RPVST+ Load Balancing Example

- The Access Layer switches have PCs attached in multiple VLANs
- CD1 is made the Root Bridge for VLANs 10-19
- Traffic for these VLANs is forwarded on the link to CD1 and blocked on the link to CD2
- CD2 is made the Root Bridge for VLANs 20-29
- Traffic for these VLANs is forwarded on the link to CD2 and blocked on the link to CD1


- **MSTP: Two Spanning Tree instances run, one for each group of VLANs for**
- **PVSTP+and RPVST+: Twenty Spanning Tree instances run for , one for each VLAN**

![[../attachments/Pasted image 20260220173948.png]]

## Spanning Tree Version Configuration

```IOS
spannning-tree mode ?
show spanning-tree summary
```

`pvst` and `rapid-pvst` use the same commands


| 802.1D  STP | RSTP, MSTP, PVSTP+, and RPVST+ |
| ----------- | ------------------------------ |
| Root        | Root                           |
| Designated  | Designated                     |
| Blocked     | Alternate                      |

# Verification - `show spanning tree`

```
show spanning-tree vlan {}
```

Root ID section gives you information about the Root Bridge
Bridge ID section gives you information about the switch

# Verification - `show mac address-table`

check that traffic is going out the expected interfaces

# Manipulating the Root Bridge

## The  Root Bridge Selection 

- Because Spanning Tree selects paths pointing towards the root bridge, it acts as a center point of the LAN. Best practice is to ensure a pair of high end core switches are selected as the first and second most preferred Root Bridge
- You can manipulate the Root Bridge election by setting Bridge priority. The default value is 32798 with the lowest number being the most preferred. In the case of a tie the switch with the lowest MAC address will be selected. This is liable to be the oldest switch

## Root Bridge Primary Configuration

```IOS
spanning-tree vlan 1 root primary
```

This command will set the Bridge Priority to 24576

## Root Bridge Failover

If the Core 1 switch fails, we want to ensure traffic still goes through the most direct centralized path

```IOS
spanning-tree vlan 1 root secondary
```

This command will set the Bridge Priority to 28672

## `spanning-tree vlan {id} priority`

You can use an alternate to primary and secondary by setting an exact number for the priority. It has the same effect of setting primary and secondary

```IOS
spanning-tree vlan 1 priority  28672
spanning-tree vlan 1 priority  24576
```

Valid values are 0 - 61440. The values must be an increment by 4096

# Spanning Tree and HSRP Alignment

HSRP should be configured to match the Spanning Tree path

# Portfast, BDPU Guard, and Root Guard

## Spanning Tree Portfast

- When a port becomes active it takes STP 30 seconds by default to ensure it will not form a loop and transition it to a forwarding state
- A device needs at least two bridges LAN connections to form a Layer 2 loop
- There isn't really any need for end hosts to wait 30 seconds before forwarding. You can make a port you are sure will never form a loop transition to a forwarding state immediately with portfast

```IOS
interface {}
spanning-tree portfast

(global) spanning-tree portfast default
```

## Portfast on Trunk Ports

- Portfast ports are typically access ports connected to end hosts
- Trunk ports are typically connected to other switches and should not have port fast enabled
- However, switchports connected to some specialized hosts such as RoaS or special virtualized hosts such as VMware are configured as trunk ports to carry multiple VLANs and should also be configured as trunk ports

```
spanning-tree portfast trunk
```

## Spanning Tree BPDU Guard

- It is best practices to enable portfast for end hosts which will not form a loop'
- Spanning Tree still runs when portfast is enabled
- If a loop is created on a portfast port, it can take Spanning Tree time to detect this and block the port. A broadcast storm can occur in this time and crash the switches

You can enable BPDU Guard on Portfast ports to guard against this happening. If a BPDU is received on the port it will be error disabled immediately. **Switches send BPDUs, end hosts do not**
<span style="color:rgb(255, 0, 0)">BPDU Guard is always used in conjunction with portfast</span>

```
interface {}
spanning-tree portfast
spanning-tree bdpuguard enable

(gobal) spanning-tree portfast bdpuguard default
```

## Bring Errdisabled Ports Back Online

Correct the issue first, then run `shutdown` and `no shutdown` to bring an error disabled port back into service

You can also configure error disabled recovery to automatically brings back ports back into service after a time period in seconds
This is not recommended because it will cause the port to flap up and down until the cause id corrected 

```IOS
errdisable recovery cause bdpuguard
errdiabled recovery interval 30
```

## Spanning Tree Root Guard

Spanning Tree Root Guard prevents an unintended switch from becoming the root bridge
If a port where Root Guard is enabled receives BPDUs that are superior than the current root bridge, it will transition the port to root-inconsistent and not forward any traffic over that port
Once the issue is corrected and superior BPDUs stop coming in, the port will transition through normal STP states


```
interface {}
spanningl-tree root guard
```

<span style="color:rgb(255, 0, 0)">Enable this on interfaces that are pointing to the switch(s) that  you do not want to become root (downstream traffic from root and backup root)
</span>

When this kicks in, it will blackhole traffic. You will have to discover and fix the issue before communication is restored

## Portfast Edge

- Portfast Edge ports transition to a forwarding state immediately
- If the port receives a BPDU, it will immediately lose its edge port status and become a normal spanning tree port. The connection stays up but it stops it from being a PortFast port. This different than BPDU Guard which error disables the port if a BPDU is received, effectively shutting it down

# BPDU Filter

Switches send BPDUs, end hosts do not
BPDU Filter is similar to BPDU Guard in that it detects unexpected BPDUs. BPDU Guard error disables ports which receive a BPDU. BPDU Filter filters out BPDUs on ports but does not disable them

## Spanning Tree BPDU Filter

BPDU Filter works differently depending on global or interface level config

- Global: applies to PortFast interfaces. Sends initial BPDUs then stops sending them. If a BPDU is received it removes PortFast, disabled BPDU filtering and acts as a normal interface which will detects loops. Similar effects to PortFast edge
- Interface: will not send BPDUs and will ignore incoming BPDUs. In effect this disables Spanning Tree

It is NOT typically recommended to enable BPDU Filter. A use case is if you have a single downstream connection to a legacy switch which is causing STP issues

```IOS
(global) spanning-tree portfast bpdufilter default

interface {}
spanning-tree bpdufilter enable

```

# Loop Guard

## Unidirectional Link Problem Example

- Many Cisco switches support Gigabit Interface Converter / Small Form-Factor Pluggable (GBIC/SFP) ports. These are copper or fiber transceivers and are typically used for switch to switch connections
- Fiber cables typically have on strand for sending data and another for receiving, with the opposite order on the other side. If one strand fails, it results in a unidirectional link failure. The interface status can still show up/up but data (including BPDUs) can only be transmitted in one direction
- When a port that is a Non-Designated/Blocking port is Up and not receiving BPDUs it becomes a forwarding designated port. This is because it no longer sees itself as the inferior route
- This would cause two Designated Ports sending traffic to each other, causing a one way loop

## Unidirectional Link Problem Solution

Ways to prevent this problem:

Loop Guard: Spanning Tree feature available in PVST+, RPVST+, and MST
Unidirectional Link Detection (UDLD): Layer 2 protocol which is not part of Spanning Tree

## Loop Guard Root and Non-Designated Ports

- BPDUs are expected to be received on Root Ports and Blocking Ports
- If BPDUs are not received on a Loop Guard protected Root Port or Blocking Port, it will be placed in the loop inconsistent state with all traffic blocked (rather than becoming a Designated Port)
- Loop Guard also protects against software failure or data corruption preventing BPDUs being sent on a link
- The port is automatically re-enabled when BPDUs are received again

```IOS
(global) spanning-tree loopguard default

interface {}
spanning-tree guard loop
```

## Loop Guard on Designated Ports

- BPDUs are not expected to be received on Designated Ports
- Loop Guard can be enabled on an Designated Port interface but it will take no action when a BPDU is not received because Designated Ports are not supposed to receive them
- End hosts do not send BPDUs. There is no issue if Loop Guard is enabled on a port connected to an end host because it will be a Designated Port

## Loop Guard and Root Guard

- Root Guard prevents undesired switches from becoming the Root Bridge. It prevents Designated Ports from becoming Root Ports
- Loop Guard does the exact opposite. It prevents Non-Designated (Root and Blocking) Ports from becoming Designated
- This means these features are mutually exclusive on ports. If Loop Guard is enabled on a port, it disables Root Guard on the port
- **If you want to enable both on the same switch, configure them at the interface level (do not use `spanning-tree loopguard default` )**

`show spanning-tree summary`
`show spanning-tree interface {}`

# PVST+ vs RPVST+ Convergence

## 802.1D and PVST+

802.1D and PVST+ use the same timer based mechanisms to build loop free paths and converge when there is a topology change
	- 802.1D uses a single STP instance for all VLANs, PVST+ uses separate instances per VLAN
	- PVST+ supports proprietary Cisco features such as PortFast, UplinkFast, BackboneFast, Root Guard and Loop Guard

### 802.1D and PVST+ Port States

- **Disabled**: Port is down
- **Blocking**: If there has been a link failure in the topology and a port has failed over to a forwarding state, it can remain in this state for **up to 20 seconds by default**
- **Listening**: Transitional state. Can send and receive BPDUs. Does not forward traffic, does not learn MAC addresses. **Forward Delay timer 15 seconds by default**
- **Learning**: Transitional State. Can learn MAC addresses, does not forward traffic. Forward **Delay timer 15 seconds by default**
- **Forwarding**: Forwards traffic. **Occurs after 30 seconds** (Listening and Learning time) by default. Portfast skips listening and learning states

A port coming online can take up to 30 second to become forwarding by default and up to 50 seconds to converge following a link failure. This is unacceptable in modern networks
## RSTP, RPVST+ and MSTP

RSTP, RPVST+ and MSTP use the same timer based mechanisms to build loop free paths and converge when there is a topology change
	- RSTP uses a single STP instance VLAN
	- RPVST+ uses separate instances per VLAN
	- MSTP groups multiple VLANs into spanning tree instances

- RSTP, RPVST+ and MSTP have equivalent convergence to UplinkFast, BackboneFast built-in, the features do not need to be enabled
- RPVST+ supports protection features such as Root Guard and Loop Guard
- RSTP/MSTP Edge Port features correspond with PortFast in RPVST+
- 
### RSTP Proposal/Agreement Handshake

- Switches actively negotiate directly with each other that ports can safely transition to forwarding states without the need for timers
- Rapid convergence (typically within a few seconds) is achieved across the STP topology

## Cisco Supported Versions

Most modern switches support PVST+, RPVST+, MSTP
PVST+ is the default on most Cisco switches but you want to change that to RPVST+

```
spanning-tree mode rapid-pvst
```

Version Interoperability - New/Old Versions

Newer Spanning Tree versions are backwards compatible with older version
Newer versions detect older versions based on Protocol Version ID number and BPDU Type fields in the received BPDUs
STP falls back to the older version on ports connected to switches running the older version. The newer version enhancements are not available on those ports. Therefore you will not have the fast convergence time that the new versions have

# RPVST+ and Hub Interoperability 

**Point-to-point Port**: Automatically assigned to full duplex links
**Shared Port**: Automatically assigned to half duplex links
RSTP Sync rapid convergence is only supported on full duplex point-to-point

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

## Redundant Link With Hub Between Switches

- RSTP Backup ports are standbys of the Designated port on a shared segment (ie with a hub)
- They do not support immediate failover. Rapid convergence is only supported on full duplex point-to-point links
- Hubs are no longer used in modern networks so you are very unlikely to see a backup port

BDPU Filter and RPVST+ and Hub sections are not used real world but may be covered on the test

# References
