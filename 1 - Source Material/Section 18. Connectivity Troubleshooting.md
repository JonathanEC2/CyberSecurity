2026-01-22 18:33
Tags: [[]]

# Basic Connectivity Troubleshooting

## Ping Responses

Five ! - success
Five . - Failed
Five U - Unreachable, possibly discarded by ACL

### Extended Ping

Ping uses outgoing interface as the source IP address

Just type `ping` for extended ping

MTU - Maximum Transmission Units 
# Traceroute

- Traces path that traffic is taking across the network
- Utilizes TTL field. It is a loop prevention mechanism. TTL is decremented by 1 every time it passes through a router


Troubleshoot on router where the traffic is stopping
Ctrl-Shift-6 to abort

# Other Troubleshooting Tools
## Layer 1 

- show ip interface brief
- show interface
## Layer 2 

- show arp
- show mac address-table

## Layer 4 

- Telnet

## DNS

- nslookup
- Ping by FQDN


## References
