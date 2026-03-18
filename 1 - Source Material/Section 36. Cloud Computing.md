2026-03-13 14:44
Tags: [[]]

# Traditional IT Deployment Models

## On Premise Solution Characteristics

- All equipment is located in your building and owned by you
- Clear lines of demarcation 
- New equipment will take over a week to deploy
- Equipment is CapEx
- Equipment requires technology refreshes
- You need to consider redundancy

## Colocation Facilities

- Owner of facility rents out space to external customers
- Facility owner provides power, cooling, and physical security for their customers server, storage, and networking equipment
- Desktops will still be in your offices
- Independent colo providers offer customers network connectivity options through a choice of network service providers

## Colo Solution Characteristics

- Colo provider owns the data center and is responsible for providing highly available power, cooling, and physical security according to the SLA
- You own the server, storage, and networking in the colo facility
- The connection between your offices and the colo are your network service providers responsibility
- Equipment with the colo facility is a CapEx cost
- Monthly colo hosting fees are OpEx expense
- Takes a week to deploy
- Equipment requires technology refreshes
- You need to consider redundancy

# Defining Cloud Computing

Cloud computing is a model of **on-demand** delivery of IT resources—such as servers, storage, databases, and software—over the internet with pay-as-you-go pricing

## Rapid Elasticity

Ability to scale outward or inward on demand, can be appropriated in any quantity at any time

## Broad Network Access

Should be able to be accessed anywhere from the companies office or anywhere on the Internet, as well as support from a variety of different clients

## Resource Pooling

Resources are shared which brings cost down
## Measured Service

Cloud systems automatically control and optimize resources used by leveraging a metering capability at some level of abstraction appropriate to the type of service

# Cloud Computing Case Study

Auto scaling can monitor how busy the servers are in AWS, and if it goes above a certain threshold, it can automatically spin up additional servers.

Security Group is where you configure firewall rules

# Server Virtualization

## Virtualization

- One of the main enablers of Cloud Computing
- It allows for resource pooling where multiple customers share the underlying hardware
- Redundancy id supported by adding multiple physical systems which each have virtual systems running on them

## Before Virtualization

![[attachments/Pasted image 20260313155525.png]]

Every server runs on its own 
Server Utilization is around 15%
You'd have to pay for each separate server

## Server Virtualization

### Type 1 Hypervisor

![[attachments/Pasted image 20260313155722.png]]

Type 1 hypervisor runs directly on the system hardware
You install virtual machine on top of the hypervisor 
If a problem occurs in a virtual machine, it will only affect that one device
Best used for data centers

Popular Type 1 Hypervisors:
- VMware ESXi
- Microsoft Hyper-V
- Red Hat KVM
- Oracle VM Server

### Type 2 Hypervisor

![[attachments/Pasted image 20260313160337.png]]

Have a normal desktop OS running on top of the hardware along with other applications with the  hypervisor being installed on the OS as well


Popular Type 2 Hypervisors
- VMware Workstation
- VirtualBox

## Containers

![[attachments/Pasted image 20260313161338.png]]

Similar to virtual machines but they virtualize software layers above the OS level. They are software packages that contain an application or microservice and the dependencies required to run it (system executable, libraries)


- Lightweight
- Fast to provision
- Highly portable across different machines and environments
- Docker is the most well known container engine

# Virtualizing Network Devices

Virtual Switch

![[attachments/Pasted image 20260313161945.png]]

Switch in red is virtual
Would configure trunk ports between both switches

## Virtual Router

![[attachments/Pasted image 20260313162129.png]]

## Firewall Virtualization with Context

![[attachments/Pasted image 20260313162454.png]]

- Contexts act as completely separate firewalls
- You could also give the customers access to manage their own devices because they have got separate configurations

## Router Virtualization with Virtual Routing and Forwarding (VRF)

![[attachments/Pasted image 20260313162620.png]]

- Separate routing tables for different customers and/or different departments
- You couldn't give the customers own administrators access to the router or to configure it because there is a single configuration.
- Most common in MPLS

## Clustering

Combines multiple physical systems into a single virtual system
Provides redundancy and increased performance

# Cloud Service Models

## Infrastructure as a Service (IaaS)
![[attachments/Pasted image 20260313222903.png]]

## Platform as a Service (PaaS)

![[attachments/Pasted image 20260313223442.png]]

Typically used for developing software
Platform as a Service, will usually have plugins  that you can pull into your own application  (plugins for e-commerce like payment systems). Rather than  having to write the entire code from scratch, you get into this custom environment and you can pull pieces of code in to build your own applications
## Software as a Service (Saas)

![[attachments/Pasted image 20260313223458.png]]

Access software directly from a web portal rather than having to install and manage it

# Cloud Deployment Models

## Public Cloud

Open use by the general public

Examples:
- AWS
- Azure
- Salesforce

## Private Cloud

- Provisioned for **exclusive use by a single organization** comprising multiple consumers. May be owned, managed, and operated by the organization, a third party, or a combination
- Works the same way as public cloud but services are provided to internal business instead of external public enterprises
- NOT SHARED WITH ANY OTHER CUSTOMERS
- Private cloud is mostly suitable for large companies where the long term ROI and efficiency gains outweigh the initial effort and cost to set up the infrastructure and automated workflows

## Community Cloud

- Provisioned for exclusive use by a specific community of consumers from organizations that have shared concerns
- Least common

## Hybrid Cloud

- Composition of two or more distinct could infrastructure  (private, community, or public) that remain unique entities but are bound together by standardized or proprietary technology that enables data and application portability
- Companies with limited Private Cloud infrastructure may 'cloud burst' into public cloud for addition capacity when required
- A company could also have Private Cloud at their main site and use Public Cloud for their Disaster Recovery location

# Cloud Computing Advantages

 - **Scalability** - Can scale up and down as needed
- **Cost Efficiency** - Pay what you need resulting is direct proportional costs. Customer does not have depreciable hardware assets
- **Competitive advantage** - reducing capital spent on infrastructure releases funds to invest in innovation or other priority areas
- **Productivity** - IT staff can focus more on strategic decisions and developing and improving core apps rather than maintaining or troubleshooting hardware infrastructure
- **Availability and Reliability** - All major Cloud Providers facilities are located in hardened data centers with redundant power, no single points of failure and onsite security. Service will be certified to the relevant industry standards such as ISO 9001 (Quality) and 27001 (Security)
- **Cost** - decision to deploy cloud usually comes down to the overall long term cost. Total Cost of ownership (TCO) of maintaining an On Prem solution should be compared to the TCO of maintaining a could equivalent and the advantages and disadvantages of each. Most companies do a mix of On Prem and Cloud
## References
