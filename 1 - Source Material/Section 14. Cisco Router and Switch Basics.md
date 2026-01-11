2025-12-30 14:04
Flashcards:
Source: [[]]
Tags: [[]]

# Basic Router and Switch Configuration

## Router IP Addresses

Routers provide connectivity between different IP subnets

```IOS
interface {interface name}
ip address {ip address} {subnet mask}
no shutdown
```

## Switch Management IP Address

- A Layer 2 switch is not IP address aware. It does however support a single IP address for management
- The IP address and subnet mask is configured on the Switched Virtual Interface (SVI) for the default VLAN
- A default gateway also needs to be configured to allow connectivity to other subnets

```IOS
interface {interface name}
ip address {ip address} {subnet mask}
no shutdown
exit
ip default gateway {ip address}
```

Additional commands need to be entered to be able to use Tenet or SSH, see section

## Hostname

`hostname {hostname}`

## Description

Descriptions can aid in troubleshooting

`descritption {description}`

# The Setup Wizard

Enable secret is used to protect access to privileged exec and configuration modes, encrypted
Enable password is similar to enable secret but not encrypted
Virtual terminal password is used for incoming telnet or SSH session

# Speed and Duplex Settings

- Interface speed and duplex are set to auto by default. Both sides should auto negotiate to full duplex and the fastest speed available
- Best practice is to set the speed and duplex on ports which are connected to another network infrastructure device or server. It is very important to set matching speeds and duplex settings on both sides of the link (manual on both sides or auto on both sides)

```IOS
interface {interface name}
duplex full
speed {speed}
```

# CDP and LLDP

## CDP Cisco Discovery Protocol

- Cisco Discovery Protocol is a Cisco Proprietary Layer 2 protocol. It is used to share information with other directly connected Cisco equipment such as OS version and IP address. This aids in troubleshooting by allowing administrators too map out how Cisco devices are connected to each other
- Enabled on most devices by default
- Operates at Layer 2 so no IP address is needed

`cdp run` runs cdp
`no cdp run` disables cdp
`no cdp enable` entered at the interface level to prevent certain interfaces from using cdp
`show cdp` will show if cdp is enabled or not 
`show cdp neighbors`  brief summary view of neighbors
`show cdp neighbors detail` detailed view

## LLDP Link Layer Discovery Protocol

LLDP is an open standard protocol, provides similar info to CDP

Differences:
- May be disabled by default 
- Is only supported on physical interfaces
- Can only discover one device per port
- Can discover Linux servers

`lldp run` runs lldp
`no lldp run` disables lldp
`no lldp transmit` entered at the interface level to prevent certain interfaces from transmitting
`no lldp receive` entered at the interface level to prevent certain interfaces from receiving
`show lldp` will show if lldp is enabled or not 
`show lldp neighbors`  brief summary view of neighbors
`show lldp neighbors detail` detailed view

# Basic Layer 1 and 2 Troubleshooting

## Layer 1 Troubleshooting

- Interface is administratively shut down
- Cable is disconnected on either or both ends
- Device is powered off
- EMI

## show ip interface brief

`show ip interface brief`

'administratively down' - issue 'no shutdown'
'down/down' - Layer 1 issue, check interface cables and power
'up/down' - Layer 2 issue or speed mismatch, check interface config on both sides of link

## show interface

`show interface`

If the interface is reporting an excessive amount of errors it could be a Layer 1 or 2 issue

## Speed and Duplex Mismatches

Incorrect speed settings can cause the interface to operate below its maximum speed. Speed mismatches will typically bring the interface down
The interface will typically stay up with duplex mismatches but will have bad performance because of collision
`show interface` will report high number of errors in this case

## References
