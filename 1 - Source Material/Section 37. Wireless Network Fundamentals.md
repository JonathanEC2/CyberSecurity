2026-03-14 14:02
Tags: [[]]

# Wireless Network Types

## 802.11 

WIFI services are defines in the Institute of Electrical and Electronic Engineer (IEEE) 802.11 standard

## Wireless Network Types 

<b><u>Wireless Personal Area Network</u></b>
Wireless Personal Area Network
Devices are within 10 meters of each other
Bluetooth is often used

<b><u>Wireless Local Area Network</u></b>
Provides access to a campus (typically wired) network, without the need for a cable
Devices within 100m of an access point

<b><u>Wireless Metropolitan Area Network</u></b>
Covers a large area such as a city

## Ad-hoc vs Infrastructure Mode

- Ad-hoc  - Two or more wireless station communicate directly with each other; Independent Basic Service Set
- Infrastructure - Stations communicate via Wireless Access Point (WAP).  This can provide access to a wired network. Multiple APs can be deployed to provide the required coverage

Wireless stations work in either Ad-Hoc or Infrastructure Mode, They can not operate in both at the same time using 

## WIFI Direct 

Allows devices to connect to an Access Point and also be part of a peer to peer wireless network
It does not support Ad-Hoc IBSS mode, it is an extension to Infrastructure Mode
WPS enables connection setup by pushing a button 
It is WPAN 

## Wireless Bridges

Can be used to connect areas which are not reachable via cable to the network

## Mesh Networks

Deployed to spread the coverage area of a WLAN 
One AP radio is used to serve clients, The other radio connects to the backhaul network 

# Infrastructure Mode and Wireless Access Points

## Wireless Access Points

- WAPs provide connectivity between wireless stations and between the wireless and wired networks 
- Wireless is half duplex, only one device can communicate at a time

**Basic Service Set (BSS)** - An AP centralizes access and control over a group of wireless devices. The devices and their wireless settings make up the BSS
**BSSID** - Devices within BSSs are identified by their BSSID, which is based on their MAC address
**Distribution System** - connects WAPs to the wired network 
**Basic Service Area (BSA)** - wireless coverage of an AP
**Service Set ID (SSID)** - Unique identifier that names the wireless network
## Multiple SSID 

A single AP can support multiple SSIDs
For example, 'Corporate' and 'Guest'
Different SSIDs can have different security settings and be mapped to different VLANs
## Beacons

WAPs broadcast info about their WLANs (including SSID and authentication requirements) with beacon frames
Can be disabled to prevent people from discovering network

## Extended Service Set

The same SSID can be supported across multiple APs to give larger coverage area
Roaming - Wireless client stations can roam across WAPs supporting the same WLAN

# Wireless LAN Configurations and CAPWAP

## Wireless LAN Controllers (WLC)

Configuring a large amount of APs one by one becomes unmanageable
WLC can be used as a central point of management

## WLC Interfaces

| Interface        | Primary Function                                                                                                                                                     |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Management**   | Used for in-band management (GUI/SSH) and for Layer 2 LWAPP communications.                                                                                          |
| **AP-Manager**   | Controls all **Layer 3 communications** between the WLC and lightweight APs once they have joined the controller.                                                    |
| **Virtual**      | Supports mobility management, DHCP relay, and guest web authentication. It is not a physical port.                                                                   |
| **Service Port** | Used for **out-of-band management** and system recovery; it is the only interface available during the boot process. Default gateway cannot be assigned through DHCP |
| **Dynamic**      | User defined and typically used for client data                                                                                                                      |
## Autonomous vs Lightweight APs

- Standalone APs are know as autonomous APs
- Access Points with A WLC are known as Lightweight APs
- The installed software image determines whether an AP is Autonomous or Lightweight

## Zero Touch Provisioning

Lightweight APs support Zero Touch Provisioning
They discover the Wireless LAN controller via:
- DHCP - option 43 gives the IP address of the WLC
- DNS - cisco-capwap-controller resolves the IP address of the WLC
- Local subnet broadcast; if you're wireless LAN controller is on the same IP subnet and VLAN as a wireless access point, the wireless access point can find it by doing a broadcast.

## Roaming with WLC

- If you are roaming with APs that require encryption but do not use a WLC, there will be a break in service because authentication is handled separately on each device
- Using a WLC, authentication is offloaded from the AP to the WLC
## WAPs

- The lightweight AP downloads its configuration from the WLC which includes what WLANs it should support and their settings
- The WLC also monitors the wireless quality and controls the channels and power of the APs
- Can detect rouge APs

## Control and Provisioning of WAPs (CAPWAP)

- CAPWAP enables WLCs to manage a collection of WAPs
- Communications are encrypted inside a DTLS CAPWAP tunnel
- It uses UDP ports 5246 and 5247
- Management traffic between the AP and WLC also passes through the CAPWAP tunnel
- Etherchannel is often used on the WLC to switch link

## Split MAC

Work is moved form the APs to the WLC which is why they are called Lightweight APs
Real-time traffic is still handles by the AP in order to provide suitable performance, the rest is handled by the WLC
This is known as Split MAC

### Split MAC - AP operations 

- Client handshake 
- Beacons
- Performance Monitoring
- Encryption and decryption
- Clients in powersave

### Split MAC - WLC operations 

- Authentication
- Roaming control
- 802.11 to 802.3 communication
- Radio Frequency management
- Security management
- QoS managements

## FlexConnect

Traffic is forwarded locally when FlexConnect is configured
Packet will not go over CAPWAP tunnel if traffic is in the same area
Useful for small branch offices without a WLC

# Switch Configuration

## Autonomous AP

AP will be tagging the frames and sending them on the switch. Because there is different traffic going for different VLANs, we will need to have a t**runk configured between the AP and the switch** to support those different VLANs

![[attachments/Pasted image 20260314152941.png]]

VLAN  Config
```
vlan 21
vlan name Corporate
vlan 22
vlan name Guest

interface {}
switchport trunk encap dot1q
switchport mode trunk
switchport trunk allowed vlan 21,22
```

## CAPWAP Config

Wireless AP does not handle tagging with CAPWAP deployed. Port from AP to switch will be an access port, port form switch to WLC will be trunk port

![[attachments/Pasted image 20260314153514.png]]

```
vlan 21
vlan name Corporate
vlan 22
vlan name Guest
```

- Because we are using a WLC, we need to configure VLAN for management as well
- VLAN 11 WLC-Management is for the administrator to manage the wireless LAN controller
- VLAN 10 is for traffic between the access points and the wireless LAN controller (CAPWAP traffic)
```
vlan 10
name WLC-Management
vlan 11
name AP-management
```

Configure interface connected to the WLC as a trunk from the management and WLAN VLANs
```
interface {}
switchport trunk encap dot1q
switchport mode trunk
switchport trunk allowed vlan 10,11,21,22
```

Configure interface connected to the AP as an access port in the AP management VLAN
```
interf {}
switchport mode access
switchport access vlan 11
```

# Wireless Channel Radio Frequencies

## WIFI Spectrum

Wifi services operate in the 2.4 and 5 GHz frequency spectrum. This is allocated for industrial, scientific, and medical (ISM) use
ISM devices do not have regulatory protection against interference from other users of the band

## IEEE 802.11 Standards

|                   | 802.11 | 802.11a                      | 802.11b    | 802.11g                                       | 802.11n   | 802.11ac   | 802.11ax   |
| ----------------- | ------ | ---------------------------- | ---------- | --------------------------------------------- | --------- | ---------- | ---------- |
| Frequency         | 2.4    | 5                            | 2.4        | 2.4                                           | 2.4 and 5 | 5          | 2.4,5,6    |
| Data Rate im Mbps | 1,2    | 6, 9, 12, 18, 24, 36, 48, 54 | 1,2,5.5,11 | 1, 2, 5.5, 11<br>6, 9, 12, 18, 24, 36, 48, 54 | Up to 600 | Up to 3500 | Up to 9608 |
Each is backwards compatible at the same frequency
## 2.4 GHz Spectrum

- Ranges from 2.4 to 2.4835
- Th spectrum is divided into smaller (22 MHz) ranges of frequencies called channels
- Each AP operated in one channel
- Some channels overlap  can cause interference with each other
- Access points with overlapping service area should use non-overlapping channels

![[attachments/Pasted image 20260315110837.png]]

## 5 GHz Spectrum

- 5 GHz channels are 20 MHz wide
 - They have less overlap than 2.4 GHz
 - Neighboring APs should be separated by at least one channel
 - Channel can be bonded (20,40, or 160 MHz wide) to multiply data rates by 2, 4, or 8

![[attachments/Pasted image 20260315111422.png]]

## 2.4 vs 5 GHz

2.4 has greater range and better propagation through obstacles
2.4 is more crowded
5 GHz has higher throughput than is available with 2.4 GHz
More support for 2.4 MHz

## Site Survey

- Site surveys should be carried out for WIFI networks
- This is to find the best placement of APs for maximum coverage of the area and minimum leakage outside. It should also discover potential sources of interference
- A WLC can manage channel allocation and power levels

# Wireless Security

WIFI coverage can leak outside the desired area
Strong authentication and encryption techniques should be used

## Wireless Security Standards

- Wired Equivalent Privacy (WEP) - RC4 encryption
- WIFI Protected Access (WPA)  - RC4,  TKIP
- WPA2 - AES encryption, Counter Cipher Mode with Block Chaining Message Authentication Code (CCMP)
- WPA3 - AES encryption, CCMP, protection against KRACK

## WPA Personal and WPA Enterprise

- WPA Personal uses pre-shared keys
- WPA Enterprise uses an AAA server

Cisco Centralized Key Management (CCKM) enables a wireless client to roam from one access point to another without intervention from the WLC
# LAB

<b><u>Switch Configuration</u></b>
Configure VLAN
Configure DHCP (excluded addresses, pool, default router, DNS)
Option 43 for WCL `option 43 ip {}`
You can configure DHCP on WCL so you don't need to do it for Management VLAN
Configure trunk port to WLC (allowed VLANs)
Spanning Tree portfast

<b><u>Wireless Network Configuration</u></b>
Configure WCL with IP address
Integrate it with AAA server
Configure DHCP scope
Configure Virtual Interface
Configure LAN (Security)
Enable status
## References
