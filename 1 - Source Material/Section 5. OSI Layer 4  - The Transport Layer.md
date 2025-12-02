2025-11-12 15:13
Status:
Flashcards:
Source: [[]]
Tags: [[OSI]] 


## Transport Layer

Transport layer is responsible for end to end error recovery and flow control. **Flow control** is the process of adjusting the flow of data from the sender to ensure receiving host can handle it all.

## Session Multiplexing 

**Session multiplexing** is the process in which a host is able to support simultaneous sessions and manage the individual traffic over a single link

## Layer 4 Port Numbers

Layer 4 destination port number is used to identify the upper layer protocol

The sender also adds a source port number to the Layer 4 header. The combination of source and destination port numbers can be used to track sessions

## TCP 

- TCP is connection oriented - once a connection is established, data can be sent bidirectionally over that connection 
- TCP carries out sequencing to ensure segments are processed in the correct order
- TCP is reliable - lost segments are resent
- TCP performs flow control

SYN - SYN/ACK - ACK

## TCP Header

![[attachments/Pasted image 20251112150948.png]]

## UDP

- UDP sends traffic best effort
- UDP is not connection oriented, no handshake, does not perform sequencing, is not reliable, and does not perform flow control. If error detection is needed, it is up to the upper layers to provide it

## UDP Header

![[attachments/Pasted image 20251112151421.png]]

## TCP vs UDP

- Applications that require reliability will use TCP. Real-time applications such as voice and video can't afford the extra overhead so they use UDP
- Some applications use both


## References