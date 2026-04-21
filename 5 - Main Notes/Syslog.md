2026-04-06 20:43
Tags: [[]]

# Syslog

Logging messages on a Cisco device comply with Syslog standards

## Syslog Format

seq no: time stamp %facility - severity - MNEMONIC : description

Oct 3 00:44:12.627: %LINK-5-CHANGED: Interface FastEthernet0/0, changed state to administratively down

## Severity Levels

![[attachments/Pasted image 20260312142557.png]]

Logging Locations

- Console line - events will be shown in the CLI when you are logged in over a console connection. All events logged by default
-  Logging buffer - events saved in RAM memory, viewed with the `show logging` command. Logged by default
- VTY Terminal lines - events will be shown in the CLI when logged in over Telnet or SSH. Not default
- External Syslog servers

## Internal Logging Locations Configuration

```
no logging console (disables logging to console line)
logging monitor 6 (events with info levels and higher will log to vty lines)
logging buffered debugging (level 7 and higher will be logged to buffer)
```

## Logging to an External Syslog Server

Set verbose logging to provide detailed troubleshooting information

```
logging {ip address}
logging trap debugging
```

## Logging Synchronous

Prevents Syslog messages from disrupting your commands

# Simple Network Management Protocol

- Open standard for network monitoring 
- Can collect and organize info from an SNMP Agent which is SNMP software which runs on managed devices such as routers
- SNMP Manager is commonly called SNMP Server or Network Management System (NMS)
- SNMP Manager can pull info from the device ('Get') or the device can push to the server ('Trap')

## SNMP Versions

- SNMPv1 uses plaintext authentication between the Manager and Agent using matching community strings
- SNMPv2c also uses plain text Community strings, supports bulk retrieval 
- SNMPv3 supports strong authentication and encryption, preferred version but not supported on all devices

## SNMPv2c

Uses community strings rather than a username and password to authenticate the SNMP Manager and Agents
Matching community strings need to be set on both sides for the Manager and Agents to communicate

## SNMPv2c Config

```
snmp-server contact {email address}
snmp-server location
(optional)

snmp-server community {} ro
snmp-server community {} rw

snmp-server host {ip address} {name}
snmp server enable traps config
```

## SNMP Security Best Practice

- Best practice is to disable SNMP on devices where it is not used
- Use SNMPv3 with secure passwords on devices where it is used. If it is not supported, use non-default Community strings

# SNMPv3 Configuration

- SNMPv3 supports authentication and encryption, it works with users and groups
- A matching user account is set up on the NMS server and network device
- Settings are derived from the group the user is a member of

## SNMPv3 Security Levels

noAuthnoPriv - no authentication password is exchanged and the communication between the agent and the server are not encrypted
AuthnoPriv - Password authentication is used, no encryption is used for communication between devices
AuthPriv - Password authentication is used, communication between the agent and server are also encrypted

## SNMP Config 

### Group 

`snmp-server group {name} v3 (auth | no auth | priv) {optional}`

**Access** can be used to reference an access-list which limits the device to communicating with the IP address of the NMS server only
**Context** are used on switches to specify which VLANs are accessible via SNMP
**Views** can be used to limit what info is accessible to the NMS server
	If you don't specify a read view then **all** MIB objects are accessible to read
	If you don't specify a write view then **no** MIB objects are accessible to read

### User

`snmp-server user {username} {group} v3 (auth | no auth | priv) (sha,md5) {password} priv (3des,des,aes) (128,192,256) {password}`
## References
