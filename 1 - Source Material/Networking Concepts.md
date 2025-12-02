---
sr-due: 2025-05-12
sr-interval: 4
sr-ease: 270
---
2025-10-28 14:03
Status:
Flashcards: #review
Source: [[]]
Tags: [[../2 - Tags/Networking|Networking]] [[../2 - Tags/OSI|OSI]]


# Network Concepts

## OSI model / TCP IP Model

| Layer        | Description                                                                                                                                                                                        |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Application  | Works almost exclusively with applications, providing an interface for them to use to transmit data. **(SNMP, HTTP, FTP)**                                                                         |
| Presentation | Translates the data into a standardized format, as well as handling any encryption, compression, or other transformations to the data. **(ASCII, PNG)**                                            |
| Session      | Establishes a connection between devices **(SYN/ACK)**                                                                                                                                             |
| Transport    | Sets up direct communication between connected devices **(TCP,UDP)**                                                                                                                               |
| Network      | Responsible for routing data, and locating the destination of your request. Logical addressing **(IP, Routers)**                                                                                   |
| Data Link    | Communication between locally connected devices. checks the received information to make sure that it hasn't been corrupted during transmission. Physical addressing **(MAC addresses, Switches)** |
| Physical     | The hardware of the computer; converts the binary data of the transmission into signals and transmits them across the network **(RJ45)**                                                           |

## Encapsulation

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdaf61tj85FadV73eU6F1VmWBKEB3BaT8ZM9g3oYtk6iSZSRs-w__f0K6jEochfnIfnis7w0zF036n_EzEuR3brzqJnsemrN4_D4vj8537fEHXmK7ktd7BoA3eM1mDpzPeGiHr8yVX0TKkl7eu48yVkYStY?key=TfE_5MxENIjRvhHpOZCQ2w)

As the data is passed down each layer of the model, more information containing details specific to the layer in question is added on to the start of the transmission. For example, the header added by the **Network Layer** would include things like the source and destination IP addresses, and the header added by the **Transport Layer** would include information specific to the protocol being used. The **Data Link Layer** also adds a piece on at the end of the transmission, which is used to verify that the data has not been corrupted on transmission; has the added bonus of increased security, as the data can't be intercepted and tampered with without breaking the trailer

When the message is received by the second computer, it reverses the process -- starting at the physical layer and working up until it reaches the application layer, stripping off the added information as it goes. 

## TCP/IP Model 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfa2tW8_uNW9MtPHScVMfRnQCIk2RJAz1fn2J99DFSrhIuIVMYJ0K6JMMvMozyomwQxfmilOcBnjuVWYvp19VlKVKqi9biXxxa4dd0ZfUVdP-4wp50LjmPJyirKPYEQFs-xwG-bQbEU6zF2qegXT5w_H_A?key=TfE_5MxENIjRvhHpOZCQ2w)

## Telnet
The TELNET (Teletype Network) protocol is a network protocol for remote terminal connection. In simpler words, telnet, a TELNET client, allows you to connect to and communicate with a remote system and issue text commands

## References