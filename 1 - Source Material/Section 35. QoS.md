2026-03-12 21:38
Tags: [[]]

# QoS Overview
## Traditional vs Converged Networks

- On modern networks, data, voice and video run over the same shared infrastructure
- This enables cost savings and advanced features for voice and video. However data, voice, and video are all fighting for the same shared bandwidth

## Quality Requirements for Voice and Video

- Latency (delay) <= 150ms
- Jitter (variation delay) <= 30 ms
- Loss 1%

These are one way requirements, meaning packets sent from a phone in HQ has 150ms to reach the phone in the branch and vice versa

## First in First Out (FIFO)

- Whenever congestion is experienced on a router switch, packers are sent out FIFO
- Congestion can happen when packets come in faster than they can go out

## Effects of Congestion 

Causes delay to packets as they wait in the queue
As the size of the queue changes it causes jitter
There is a limit to the size of the queue; if a packet arrives when the queue is full the router will drop it
Voice and video calls will be unacceptable quality if they do not meet their delay, jitter, and loss requirements

## How to Mitigate Congestion 

Add more bandwidth (costs money)
Use QoS techniques to give better service to the traffic which needs it

## Effects of QoS Queuing

- 
- Original driver of QoS was VoIP but it can also be used to give better service to data applications
- If you're giving one type of traffic better service on the same link you started with, other types of traffic types must get worse service. The point is to give each type of traffic the service it requires
- QoS is meant to mitigate temporary periods of congestions. If a link is permanently congested the bandwidth should be increased

# Classification and Marking

For a router or switch to give particular level of service to a type of traffic, it has to recognize that traffic first
Common ways to recognize the traffic are by Class of Service (COS) marking, Differentiated Service Code Point (DSCP) marking, ACLs, or Network Based Application Recognition (NBAR)

## Layer 2 Marking Class of Service

- There is a 3 bit field in the 802.1q frame header which is used to carry the CoS QoS marking
- A value of 0-7 can be set. The default is 0 which is best effort
- CoS 6 and 7 are reserved for network use
- IP phones mark their calls signaling traffic as CoS 3 and their voice payload as CoS 5
- Higher value = more important

## Layer 3 Marking Differentiated Service Code Point 

- The Type of Service byte in the Layer 3 IP header is used to carry the DSCP QoS marking
- 6 bits are used which give 64 possible values. The default value is 0 which is designated as Best Effort traffic
- IP phones mark their calls signaling traffic as 24 (CS3) and their voice payload as 46 (EF)
- DSCP is the preferred classification and marking method because the router can very quickly gather the information from a single byte in the header

## The Trust Boundary

The switch should be configured to trust markings from the IP phone and pass them on unchanged, but mark traffic from the PC down to CoS 0 and DSCP 0

## Recognizing Traffic with an Access Control List

If you want to give particular QoS to another application running between workstation and a server, the endpoints typically be unable to mark their own traffic
An ACL can be used to recognize traffic based on its Layer 3 and 4 information
Configure as close to the source as possible

## Recognizing Traffic with Network Based Application Recognition

NBAR can be used to recognize traffic based on its Layer 3 to Layer 7 information
Signatures can be downloaded from Cisco which recognize well known applications
Configure as close to the source as possible
# Congestion Management

Queuing can be used to manage congestion on routers and switches
Class Based Weighted Fair Queuing (CBWFQ) gives bandwidth guarantees to specific traffic types
Low Latency Queuing (LLQ) is CBWFQ with a priority queue

## Modular QoS CLI (MQC)

It has 3 main sections
	- **Class Maps** define the traffic to take action on 
	- **Policy Maps** take the action on the traffic 
	- **Service Policies** apply the policy to an interface

priority percent - guaranteed that much and also limited to that much
bandwidth percent - guaranteed that much but can go past the amount set if available

# Policing and Shaping


- Traffic Shaping and Policing can be used to control traffic rate
- They both measure the rate of traffic through an interface and take an action if the rate is above a configured limit
- Traffic Shaping buffers any excess traffic so the overall traffic stays within the desired rate limit (typically used on customer side)
- Traffic Policing drops or remarks drops or remarks excess traffic to enforce the specified rate limit (typically used on service provider)

## Policing with Enterprise

Another use case for policing is worm and junk traffic
This is known as Scavenger traffic. The recommended value to mark it with is DSCP 8 (CS1)
Policing can be used to rate limit junk traffic down to prevent it from taking bandwidth from business applications 
## References
