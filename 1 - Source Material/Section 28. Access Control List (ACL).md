fas2026-03-03 20:09
Tags: [[]]

# Access Control List Overview

ACL identifies traffic based on characteristics of the packet such as source IP address, destination IP address, port number. The router or switch can take action depending on the result of the ACL
ACLs are supported on both routers and switches

ACLs original use was a security feature to decide if traffic should be allowed to pass through the router
ACLs are also used in other software policies when traffic has to be identified such as:
	- To give better service to in a QoS policy
	- To translate to a different IP address in a NAT policy

## Access Control Entries (ACE)

Access Control Lists are made up of Access Control Entries which are a series of permit and deny rules. Each ACE is written on a different line

```
access-list 100 deny tcp 10.10.30.0 0.0.0.255 gt 49151 10.10.20.1 0.0.0.0 eq 23
```

```
access-list {Number} {Action} {Protocol} | {IP} {Wildcard} {Qual.} {Port} | {IP} {Wildcard} {Qual} {Port}
```

# Standard, Extended and Named ACLs

Standard ACLs referenced source addresses only (Range 1-99, 1300-1999 )

```
access-list 1 deny 10.10.10.10
```


Extended ACLs check based on protocol, source address, destination address, and port number (Range 100-199, 2000-2699)

```
access-list 150 deny tcp 10.10.10.10 0.0.0.0 gt 49151 10.10.50.10 0.0.0.0 eq 23
```


- In a standard ACL the default wildcard mask is 0.0.0.0, will be the same as not specifying a wildcard mask. **Must enter a wildcard mask when specifying an IP subnet**
- There is no default wildcard mask for Extended ACLs so you must specify 

## Named ACLs

Named ACLs begin with the command `ip access-list` instead of `access-list`

```
ip access-list standard Flackbox-Demo
deny 10.10.10.10 0.0.0.0
permit 10.10.10.0 0.0.0.255
```

# ACL Syntax

```
access-list {Number} {Action} {Protocol} | {IP} {Wildcard} {Qual.} {Port} | {IP} {Wildcard} {Qual} {Port}
```

Good idea to leave remarks for ACLs

 <b><font size= 5px >Protocol</font></b>

- Use TCP or UDP if you want the ACE to apply to traffic for a particular application between a source and destination address
- Use IP if you want the ACE to apply to all traffic between source and destination address

 <b><font size= 5px >Wildcard</font></b>

Saves you from typing out wildcard mask:
- any
- host

 <b><font size= 5px >Port Number</font></b>

This is optional, defaults to any port

 <b><font size= 5px >Final Options</font></b>
 
Additional options are available after entering the destination address such as destination port, TCP flags and logging

## Verification `show access-lists`

log keyword is not required to log hit counts. It is used to log to the console or an external monitoring server

# ACL Operations

## Access Groups

- ACLs are applied at the interface level with the `access-group` command. When you are configuring ACLs, don't forget to apply them with the `access-group` command.
- ACLs can be applied in the inbound or outbound direction
- You can have a maximum of one ACL per interface per direction. You can have both an inbound and an outbound ACL on the same interface, but not 2 inbound or outbound ACL
- An interface can have no ACL applied, an inbound ACL only, outbound ACL only, or ACLs in both directions

## Access-Group Configuration

```
interface {}
ip access-group 100 out
ip access-group 101 in
```

`sh running-config` for verification

## Access Control Entry

- The ACL is read by the router from top to bottom
- As soon as a rule matches the packets, the permit or deny action is applied and the ACL is not processed any further
- Put the most specific entries at the top of the list and the less specific entries down near the bottom

## Injecting ACEs in an Existing ACL

ACEs are automatically numbered in increments of 10
If you want to inject a more specific rule in the ACE, you can put a number before the rule to specify where it is in the ACL

```
ip access-list extended 110
15 deny tcp host 10.10.10.11 host 10.10.50.10 eq telnet
```

## Implicit Deny All

There is an implicit 'deny any any' rule at the bottom of ACLs
If an ACL is not applied to an interface, all traffic is allowed. If an ACL is applied, all traffic is denied except for what is explicitly allowed

## Explicit Deny All

Many organizations include an explicit deny all at the end of ACLs to log illegal traffic

```
access-list 1 deny any log
```

## Explicit Permit All

If an ACL is applied, all traffic is denied except for what is explicitly allowed
If you want to reverse this so that all traffic is permitted except for what is explicitly denied, add a permit all statement to the end of the ACL

```
access-list 1 permit any
```

## Traffic Sourced from Router

ACLs applied to an interface do not apply to traffic which originates from the router itself

# Numbered ACL Lab

This would configure an access list and apply it to the specified interface for outbound traffic

```
access-list 1 deny 10.0.2.0 0.0.0.255
access-list permit 10.0.1.0 0.0.0.255
int {}
ip access-group {number} {direction}
```

Secure as close to the source as you can 

# Named ACL Lab

```
ip access-list {type} {name}
```

You would apply the ACL to the interface by name instead of by number

```
interface {}
ip access-group {name} {direction}
```

`sh access-list`
## References
