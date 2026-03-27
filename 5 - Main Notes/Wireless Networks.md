# Ad-hoc vs Infrastructure Mode

- Ad-hoc  - Two or more wireless station communicate directly with each other; Independent Basic Service Set (IBSS)
- Infrastructure - Stations communicate via Wireless Access Point (WAP).  This can provide access to a wired network. Multiple APs can be deployed to provide the required coverage

# WIFI Direct 

Allows devices to connect to an Access Point and also be part of a peer to peer wireless network
It does not support Ad-Hoc IBSS mode, it is an extension to Infrastructure Mode

# Wireless Access Points

- WAPs provide connectivity between wireless stations and between the wireless and wired networks 
- Wireless is half duplex, only one device can communicate at a time

**Basic Service Set (BSS)** - An AP centralizes access and control over a group of wireless devices. The devices and their wireless settings make up the BSS
**BSSID** - Devices within BSSs are identified by their BSSID, which is based on their MAC address
**Distribution System** - connects WAPs to the wired network 
**Basic Service Area (BSA)** - wireless coverage of an AP
**Service Set ID (SSID)** - Unique identifier that names the wireless network

# Wireless LAN Controllers

Multiple APs can be configured using WLCs. Wireless LAN controllers have multiple interfaces that serve different purposes

| Interface        | Primary Function                                                                                                                                                     |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Management**   | Used for in-band management (GUI/SSH) and for Layer 2 LWAPP communications.                                                                                          |
| **AP-Manager**   | Controls all **Layer 3 communications** between the WLC and lightweight APs once they have joined the controller.                                                    |
| **Virtual**      | Supports mobility management, DHCP relay, and guest web authentication. It is not a physical port.                                                                   |
| **Service Port** | Used for **out-of-band management** and system recovery; it is the only interface available during the boot process. Default gateway cannot be assigned through DHCP |
**Lightweight AP** - APs that are provisioned through a WLC
**Autonomous AP** - Standalone APs
**Embedded AP** - connects APs to a WLC that is housed in a switch stack
**Cloud Based AP** - connects to and are automatically configured by a WLC that is housed in a cloud-based system
## Zero Touch Provisioning

Lightweight APs support Zero Touch Provisioning. Lightweight APs  can discover the WLC with the following

**DHCP** option 43 gives the IP address of the WLC
**DNS** cisco-capwap-controller resolves the IP address of the WLC
If WLC is on the same IP subnet and VLAN as WAP

The lightweight AP downloads its configuration from the WLC that includes which WLANs it should support and their settings

## Control and Provisioning of WAPs (CAPWAP)

- CAPWAP is the protocol that facilitates the communication between the WLC and the APs. It enables WLCs to manage a collection of WAPs
- Communications are encrypted inside a DTLS CAPWAP tunnel
- It uses UDP ports 5246 and 5247

## Split MAC

Work is moved form the APs to the WLC which is why they are called Lightweight APs
Real-time traffic is still handles by the AP in order to provide suitable performance, the rest is handled by the WLC

## FlexConnect

Traffic is forwarded locally when FlexConnect is configured
Packet will not go over CAPWAP tunnel if traffic is in the same area
A lightweight AP functioning in FlexConnect mode can connect over a WAN link to a WLC that is located in a different location. This enables admins to manage the AP from a central location without having to deploy WLCs in each remote offic
Lightweight APs using FlexConnect can provide client connectivity even if the connection to the remote WLC is lost

# Wireless Channel Radio Frequencies

## WIFI Spectrum

WIFI services operate in the 2.4 and 5 GHz frequency spectrum. This is allocated for industrial, scientific, and medical (ISM) use

## IEEE 802.11 Standards

|                   | 802.11 | 802.11a                      | 802.11b    | 802.11g                                       | 802.11n   | 802.11ac   | 802.11ax   |
| ----------------- | ------ | ---------------------------- | ---------- | --------------------------------------------- | --------- | ---------- | ---------- |
| Frequency         | 2.4    | 5                            | 2.4        | 2.4                                           | 2.4 and 5 | 5          | 2.4,5,6    |
| Data Rate im Mbps | 1,2    | 6, 9, 12, 18, 24, 36, 48, 54 | 1,2,5.5,11 | 1, 2, 5.5, 11<br>6, 9, 12, 18, 24, 36, 48, 54 | Up to 600 | Up to 3500 | Up to 9608 |
Each is backwards compatible at the same frequency
## 2.4 GHz Spectrum

- Ranges from 2.4 to 2.4835
- Th spectrum is divided into smaller (22 MHz) ranges of frequencies called channels
- Each AP operates in one channel
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

## Wireless Security Standards

- Wired Equivalent Privacy (WEP) - RC4 encryption
- WIFI Protected Access (WPA)  - RC4,  TKIP
- WPA2 - AES encryption, Counter Cipher Mode with Block Chaining Message Authentication Code (CCMP)
- WPA3 - AES encryption, CCMP, GCMP, protection against KRACK

## WPA Personal and WPA Enterprise

- WPA Personal uses pre-shared keys
- WPA Enterprise uses an AAA server

WPA-3 Personal uses Simultaneous Authentication of Equals (SAE) to replace the use of pre-shared keys in WPA-2 Personal

Cisco Centralized Key Management (CCKM) enables a wireless client to roam from one access point to another without intervention from the WLC. It will enable clients to roam between APs without performing complete authentication all over again

# Summary