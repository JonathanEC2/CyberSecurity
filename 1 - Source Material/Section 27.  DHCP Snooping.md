2026-03-01 18:21
Tags: [[]]

# DHCP Snooping

## Rouge DHCP Server

Having a rouge DHCP server can drop your PC off the the network
When DHCP Snooping is enabled, DHCP Server responses are dropped if they don't arrive on a trusted port

```IOS
ip dhcp snooping
ip dhcp snooping vlan 10
int f0/1
ip dhcp snooping trust
```

Enable DHCP snooping on global and vlan
Configure trusted interface

# DAI Dynamic ARP Inspection

- Gratuitous ARP is an ARP update which is not in response to an actual request. It spoofs the address of a legitimate user
- When you enable DHCP snooping, the switch inspects the DHCP traffic and keeps track of which IP addresses were assigned to which MAC address. If invalid ARP traffic tries to pass through the switch, the switch drops the traffic
- DAI is not performed on trusted ports. Enable trust for non DHCP clients:

```IOS
int {}
ip arp inspection trust
```

Hosts that got their IP from DHCP:
```
ip arp inspection vlan {}
```


# 802.1X Identity Based Networking

When 802.1x is enabled, only authentication traffic (sending username and password) is allowed on switch ports until the host and user are authenticated. When the user has entered a valid username and password, the switch port transitions to a normal access port in the relevant VLAN

- Client is the supplicant, most OS's have 802.1x on it by default. Needs to be enabled in the OS
- Access switch is the authenticator. Needs to be configured on the switch
- Authentication server (Identity Service Engine)  is typically  integrated  with an Active Directory domain controller where the user database is

# Port Security

## Shutdown Unused Interfaces

Best practice is to administratively shutdown unused switch ports

## Port Security 

Enables an administrator to specify which MAC address(es) can send traffic to an individual switchport. This can be used to lock a port down to a particular host or hosts. However it is easy to spoof a MAC address
Port Security can also configure individual switch ports to allow only a specific number of source MAC addresses to send traffic in to the port. This is useful to prevent users from adding WAPs or other shared devices

```
interf {}
switchport port-security 
```

## Port Security Default Behavior 

If you configure Port Security with no additional parameters, only one MAC address is allowed to transmit on the port. **The current MAC address can be disconnected and replaced, the port is not locked down to a particular MAC address**
If a shared device is connected and multiple hosts try to transmit the port will be shut down

### Port Security Verification Defaults

`sh port-security interface {}`

## Security Violation Actions

**Shutdown** (Default): interface is errdisabled, blocks all traffic
**Protect**: unauthorized traffic is dropped, traffic from allowed addresses is forwarded
**Restrict**: Traffic from unauthorized addresses is dropped, logged, and the violation counter incremented. Traffic from allowed addresses is forwarded
**Aging**: automatically removes now invalid secure MAC addresses from the CAM table after a specific period of time

```IOS
switchport port-security violation protect
switchport port-security violation restrict
```

Error-Disabled Interfaces

To bring an error-disabled interface back into service:
- Physically remove the host with the offending MAC address
- Manually shutdown then no shutdown the interface

Can't put port security on dynamic port

# Locking Ports to Hosts with Port Security

## Maximum MAC addresses

Port security allows only one MAC address to send traffic by default. This can be increased if multiple hosts share the port

```
interface {}
switchport port-security maximum {}
```

## Manually Adding MAC Addresses 

You can statically configure allowed MAC addresses if you want to lock the port to a particular host

```
interface {}
switchport port-security
switchport port-security mac-address {}
switchport port-security maximum 1
```

## MAC Address Learning

Sticky MAC addresses add the learned MAC address to the running configuration. Save to startup config to make them permanent

```
interface {}
switchport port-security
switchport port-security mac-address sticky
```
# References
