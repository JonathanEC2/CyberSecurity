2026-03-10 20:02
Tags: [[]]

# Line Level Security

No security is configured on switch when first received
One of the first tasks is to configure security to ensure that only authorized admins can access the device

## Basic Line Level Security 

Minimal password security can be configured through the use of static, locally defined passwords at three different levels:
- **Console line**: accessing user exec mode when connecting via console cable
- **Virtual Terminal VTY line**: accessing user exec mode when connecting remotely via Telnet or SSH
- **Privilege Exec Mode**: entering the enable command

These can be used in combination with each other using the same or different passwords
With line level security, all admins log in with the same password
## Basic Console Security

Only one administrator can connect with a console cable at a time so the line number is always 0
`Login` without any keywords requires the admin to enter the password configured at the line level to log in

```
line console 0
password {}
login
```

## Basic Telnet Security

- **IOS devices do not accept incoming Telnet sessions by default**
- An IP address and virtual terminal VTY line access must be configured
- Multiple admins can connect at the same time (usually 16) , lines are allocated first come first serve
- If all configured lines are in use then additional admins will not be able to login

```
line vty 0 15
password {}
login
```

### Switch Management IP Address

Switches support a single IP address for management
A default gateway also needs to be configured to allow connectivity to other subnets

```
interface {}
ip address {}
no shut
exit
default gateway {}
```

## Exec Timeout

Admin will be logged out after 10 minutes of inactivity be default for both console and vty lines
You can edit this value with the `exec-timeout` command

```
line con {}
exec-timout 15
vty line 0 15
exec-timeout 5 30 (5 minutes 30 seconds)
```

## Securing VTY Lines with Access Lists

You can apply an access list to control access to VTY lines
This can be used to limit Telnet and SSH access to only admin workstations

```
access-list 1 permit host {}

line vty 0 15
login
password {}
access-class 1 in
```

# Privilege Exec and Password Encryption

## Enable Secret

- Enable secret is always shown in an encrypted format in the running config. This is a Type 5 password
- If both enable password and enable secret are set, enable secret supersedes the enable password. Best practice is to use only enable secret
- MD5 hash

```
enable secret {}
```

## Encrypting Passwords

- Line level passwords can also be viewed in plain text in the running config by default
- The `service password-encryption` command encrypts all passwords in the running config. When you issue the `service password-encryption` command on a Cisco device, all current and future Type 0, or clear-text, passwords are encrypted as Type 7 passwords in the device's running configuration.
- It is best practice to enable this


`service password-encryption`

Type 9 passwords use `enable algorithm-type scrypt`
### Lab

Make sure you set line password and enable secret

# Username and Privilege Levels

## Username and Level Security

More granular security can be provided by configuring individual usernames and passwords for different admins

```
username admin1 secret {}
line console 0
login local
line vty 0 15
login local
```

## Privilege Levels

- There are 16 different levels of admin access (0-15) available on a Cisco router or switch
- Usernames can be assigned a privilege level, default is 1
- You can also configure different passwords for direct access to the different privilege levels
- Admin must be logged in with that privilege level or higher to run the command

By default, three levels of privilege are used:
- Zero-level allows access to only logout, enable, disable, help, and exit
- User level (level 1) provides very limited read only access to the router
- Privilege level (level 15) provides complete control over the router. Gets enable prompt immediately upon login

```
username admin2 privilege 15 secret {}
```

## Configure Command Privilege Levels

Allow sh run to be ran at level 5:
`privilege exec level 5 show running-config`

Sets password for privilege level 15. If you don't specify a privilege level when you set the enable secret, it defaults to 15
`enable secret secret1`

Sets password for privilege level 5
`enable secret level 5 secret2`

use `enable 5` to access this level of commands

# SSH

## Telnet vs SSH

- Telnet communication is in plain text
- If someone sniffs traffic they can see all commands  you entered including username and password
- All SSH traffic is encrypted
- Best practice is to disable Telnet and only allow SSH for admin CLI access

## Enable SSH

SSH encrypts with a digital certificate. One of the attributes for the digital certificate is a domain name which needs to be set
You then need to generate a certificate
A digital certificate with a key length of 768 bits must be generated to enable SSH encryption

```
hostname
ip domain-name {}
crypto key generate rsa
transport input ssh
```

## Disable Telnet 

VTY lines are used for both Telnet and SSH connections
Access is allowed for both by default
A username is required for SSH access (line level passwords are not supported)

```
username {} secret {}
line vty 0 15
transport input ssh (telnet not added)
login local
exit 
ip ssh version 2 (limits ssh to version 2)
```

## SSH Access

`ssh -l {username} {ip address} `

# Authentication, Authorization, and Accounting

- External AAA servers can be used to centralize usernames and passwords
- Multiple AAA servers can be implemented for redundancy

- Authentication verifies someone is who they say they are
- Authorization specifies what a particular user is allowed to do
- Accounting keeps track of the actions a user carried out
- Authorization and Accounting are optional. Authentication is mandatory if Authorization and/or Accounting are used

## RADIUS and TACACS+

- The protocols which are used for AAA are RADIUS and TACACs+
- Both are open standard and many vendors support both protocols
- RADIUS is commonly used for end user level services such as VPN
- TACACS+ is commonly used for admin access on Cisco devices aa it has more granular authorization capabilities

## Cisco AAA Server 

Cisco's AAA server is the Identity Service Engine (ISE) which uses RADIUS and TACACS+

## Active Directory

- Integrate AAA server with Active Directory
- This gives you the granular control of the Cisco AAA server and still allows the use of one username and password in Active Directory

# AAA Configuration

## RADIUS

```
username {} secret {} (configure a local user in case connectivity to the AAA server is lost)

aaa new-model
radius server Server1
address ipv4 {}
key {}

radius Server2
address ipv4 {}
key {}

aaa group server radius FB-RB
server name Server1
server name Server2

aaa authentication login default group FB-RB local (first login choice will be the group, second login choice will be local if aaa server is down)
```

## TACACS+

```
username {} secret {}

aaa new-model
tacacs server Server1
address ipv4 {}
key {}

tacacs Server2
address ipv4 {}
key {}

aaa group server tacacs {}
server name Server1
server name Server2

aaa authentication login default group FB-RB local
```

# Global Best Practice

## Login and Exec Banners

Messages can be displayed in the CLI before and/or after an admin logs in to a Cisco IOS device. Most commonly used to display security warning

`banner login " `
`banner exec "`

## Disable Unused Services

This reduces the attack surface and also the load on the device
HTTPS is sometimes used by GUI admin tools but HTTP should be disabled
CDP should also be disabled in highly secure environments

```
no ip http server
no cdp run
```

## Time Synchronization 

- All servers and infrastructure devices in your network should be synced to the same time
- This aids in troubleshooting as logs will report the correct time that events occurred
- It is also required by Kerberos authentication and digital certificates. Kerberos authentication must not be further than 5 minutes out for synchronization 

## NTP 

- Servers and infrastructure devices can use their own internal clock or sync with an external NTP server
- An NTP server should be used to ensure all devices have the same time

```
clock timezone {}
ntp server {} (configures router as static client)
ntp master (configures router as server)
ntp broadcast client (can receive time from any ntp server)
ntp peer (enables NTP symmetric active mode)

show clock
```
## References
