2025-12-29 14:46
Flashcards:
Source: [[]]
Tags: [[]]

# The Cisco Troubleshooting Methodology
## Troubleshooting Methods

- Compare configurations
- Trace the path
- Swap out components

## Connectivity Troubleshooting Methods

- ping
- traceroute
- telnet

# The Cisco Troubleshooting Methodology - Lab

traceroute is a ping that sends with a TTL packet, it drop the packet when it reaches 0. We can leverage this by sending setting the TTL to a low number. This will map out the path from source to destination.

Telnet troubleshoots Layer 4 and above problems

routing table
`sh ip route`

static route command
`ip route { target network ip address} {subnet mask} {next hop ip address}`

## References
