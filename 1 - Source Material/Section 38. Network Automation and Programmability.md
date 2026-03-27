2026-03-15 16:20
Tags: [[]]

# The Benefits of Network Automation and Programmability

## Traditional Network Management

- Traditional network management consisted of using SSH to command line; copy and pasting from a text file template was common
- NMS systems use protocols such as SNMP and Netflow to gather info and report the state of the network
- SNMP can also be used to push configurations to devices but it has limited functionality
- SNMP also has security concerns

## The Issue with Traditional Network Management

- Configuring devices one at a time is inefficient
- Increases likelihood of mistakes
- Individual edits to multiple devices by different engineers over time with little version control lead to configuration drift. This can lead to inefficient troubleshooting

## Network Automation

- Reduces human machine interaction which greatly reduces the likelihood of mistakes
- It is much more scalable than configuring one device at a time
- Provides configuration and software version control
- Troubleshooting is more efficient with a system wide view and correlation between events
- Events and error codes can be acted on programmatically
- Reduces OPEX

# Python, Git, GitHub and CI-CD

## Python

Relatively easy to learn with many training resources
Human readable
Open source
Can be installed on all popular OS

## Git

Version control system for tracking 
Typically used for software development but can provide version control for any type of files
Every Git directory on every computer is a full-fledge repository with complete history and full version-tracking abilities. Because of this, code can be worked on by multiple developers at the same time

## GitHub

A Git repository hosting service which adds many of its own features
Repositories can be public or private
Repositories can be copies between users
Task management tools are available

## CI/CD

- CI - Continuous Integration
- CD - Continuous Delivery of Continuous Deployment

- CI/CD is a set of operating principles and practices that enable application development teams to deliver code changes more frequently and reliably
- Frequent changes are more efficient than rolling them up into large change windows
- The implementation is called the CI/CD pipeline

# Data Serialization 

- Data serialization is the process of converting structured data to a standardized format that allows sharing or storage of the data in a form that allows recovery of its original structure
- Allows transfer of the data between different systems, applications, and programming languages
- XML, JSON, and YAML are human and machine readable encoding formats
- Data formats are mostly interchangeable, which one you use depends on the support in the system you use and which is the easiest

## JSON

- Easier for humans to read and work with than XML
- Can be imported into JavaScript which is commonly used on the Internet
- White space has no special meaning
- Often used by RESTful APIs

## JSON Data Types 

Object
Array
String: "name":"GigabitEthernet1"
Number: "Input Errors" : 3
Boolean: "enabled": true
Null: "msec" : null
### Object

- Unordered collection of key/pair values
- Surrounded by {}
- Keys and pairs are separated by a colon :
- Each key/pair value is separated by a comma

```json
{
"name":"GigabitEthernet1",
"description":"Internet link",
"enabled":true
}
```
### Array

Ordered list of values
They are surrounded by square brackets \[ ]


## XML

Widely used across the Internet
Was designed to describe and transfer data
White space has no special meaning
\<key>Value\</key>

## YAML Aint Markup Language

Often used on Python, Pearl, and Ansible
Designed to be easily read by humans
White space (indentation) is important
Starts with ---
Key: value representation
\- represents a list

# APIs - CRUD, REST and SOAP

## Application Programming Interfaces (API)

- An API is a way for a computer program to communicate directly with another computer program
- It is typically used to perform CRUD operations
- The two main types of APIs for web services are SOAP and REST
- NETCONF and RESTCONF are APIs specifically designed to work for network device

## CRUD

| Operation | SQL    | HTTP            |
| --------- | ------ | --------------- |
| Create    | INSERT | PUT/POST        |
| Read      | SELECT | GET             |
| Update    | UPDATE | PUT/POST/PATCHf |
| Delete    | DELETE | DELETE          |
<u><b>HTTP Verbs</b></u>
Put: Update / replace a resource
Post: Create a new resource
Patch: Update / partially modify a resource

## Simple Object Access Protocol (SOAP)

- A standard communication protocol system that permits processes using different OSs like Linux and Windows to communicate
- The transport is typically HTTP(S) and the data format is always XML
- Because it is a protocol, it has strict standards to adhere to 

## Representational State Transfer (REST)

- An architecture not a protocol. It gives guidelines for the structure and organization of an API
- It supports any transport and data format
- HTTP(S) transport and JSON (or XML) data format are commonly used
- Typically faster performance and is easier to work with than SOAP

### REST Constraints (Guidelines)

- Client-server architecture: the client sends the request, server sends a response
- Uniform Interface: provides simplicity
- Statelessness: no client context is stored on the server between requests
- Cacheability: responses must define themselves as either cacheable or non-cacheable
- Layered system: any intermediary devices such as load balancers must be transparent to the client and server
- Code on demand (optional): servers can temporarily extend or customize the functionality of a client by transferring executable code
### REST Authentication Types

- No authentication
- **Basic authentication**: username and passwords sent in plain text. Insecure unless encrypted (ex over HTTPS), does not support granular permission per user
- **API Key**: uses encrypted tokens. The same user can request tokens with different permissions (such as read or write). **The server must check the API key permissions for every client request**; usually have long expiry due to statelessness
- **Bearer Token**: Basic or API Key authenticated user requests encrypted Bearer Token which automatically includes other requests. **Permissions are embedded into the token so it puts less load on server than API key**. Token is transferrable to other applications and usually has short expiry

### REST Request URL

![[attachments/Pasted image 20260315174211.png]]

Request method must be sent
Headers with key:value pair info about the request can be added
Post, Put, and Patch requests include body data

### REST Response Codes

| 1xx: Informational | 2xxx: Success                                              | 3xxx: Redirectional                                    | 4xxx: Client Error                                                                                                                                      | 5xx Server Error           |
| ------------------ | ---------------------------------------------------------- | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
|                    | - 200: OK<br>- 201: Created<br>- 204: No Content (deleted) |  - 301: permanently moved<br> - 302: temporarily moved | - 400 Bad request / malformed syntax<br>- 401: Unauthorized (identity not known)<br>- 403: Forbidden (identity known but no rights)<br>- 404: Not found | 500: Internal server error |



# Model Driven Programmability

## Data Models 

A data model is a well understood and agreed upon method to describe something.
They are formalized and defined by a centralized controller

## Yet Another Next Generation (YANG)

YANG is a data modeling language which provides a standardized way to represent the operational and configuration data of a network device

## Network Management Transport

The configuration and operational status of a network device's components and services can be remotely read or written to
NETCONF, RESTCONF, and gRPC are APIs which describe the protocols and methods for transport of network management data

## The Model Driven Programmability Stack

![[attachments/Pasted image 20260315181658.png]]

If we want to interact with the information on the router, we will use an API to pull the information to read it, or push it using NETCONF, RESTCONF, or gRPC

## NETCONF
### NETCONF Communication

![[attachments/Pasted image 20260315181923.png]]

YANG data that is encapsulated in XML and NETCONF information encapsulates that

### NETCOMF and YANG

- NETCOMF was designed as a replacement for SNMP
- NETCOMF and YANG provide a standardized way to programmatically inspect and modify the configuration of a network device
- YANG (IETF 2010) is a data modeling language which provides a standardized way to represent operation and configuration data of a network device
- NETCONF (IETF 2006) is the protocol that remotely reads or applies the changes to the data on the device
- XML coding is used
- Transport is over SSH or TLS/SSL

## NETCONF Protocol Stack

- Content - data to be inspected or changed
- Operation - (ex \<get-config>, \<edit-config>) Initiated via RPC methods using XML encoding
- Message - Remote Procedure Calls (RPC allows one system to request another system to execute code)
- Transport - between client and server; SSH or TLS/SSL

![[attachments/Pasted image 20260315182819.png]]

## RESTCONF

- Builds on NETCONF
- AN IETF draft that describes how to map a YANG specification to a RESTful interface
- Uses HTTP verbs over API
- Simpler to use than NETCONF
- XML or JSON is used
- Transport is HTTP(S)

![[attachments/Pasted image 20260315183126.png]]


## Google RPC (gRPC)

Well suited for collecting telemetry stats
Google Buffering Protocol (GBP) is used 
Transport is HTTP/2

## Postman

- Tool used to test the operations of REST APIs
- Collections and environments allow you to easily reuse requests
- Requests can be exported as code in multiple programming languages
- You can pull scripts from here and edit them for your needs

# Configuration Management Tools - Ansible and Terraform

- Configuration management systems allow you to control many different systems in an automated way from one location
- They can automate provisioning and deployment of servers and network devices
- Requires little knowledge of programming

## Ansible

Can run from any machine with Python 2 or Python 3 installed
Agentless
Push model
Communicates over SSH by default

Ansible **modules** are prebuilt Python scripts
Ansible **inventory** files define all hosts that will be managed by the control workstation
Ansible **playbooks** are YAML files that outline the instructions it needs to run
**ansible.cfg** is Ansibles default configuration file

## Puppet

- Typically uses agents on target device
- 'Puppet Master' runs on Linux
- Pull model, agents check in every 30 minutes
- Written in Ruby
- A 'Manifest' defines the devices properties

## Chef

- Agents must be installed
- Pull model
- Written in Ruby
- Terminology is Cook Book > Recipe

## Terraform

- Infrastructure as Code (IaC) software
- Admins provision infrastructure using HashiCorp Configuration Language or JSON
- Primarily designed for public and private cloud, can also work with on-prem platforms
- Agentless
- Push model
- Written in Go, can be installed on Windows, Linux or Mac
- Communicates over REST APIs, NETCONF, SSH, SNMP

### Terraform Components

- **Configuration files** determine the finale desired state using resource blocks. Resources are virtual machines, network devices, etc
- The **State file** provides lifecycle management by tracking the deployed resources
- **Providers** are plugins that interface with platforms such as AWS or IOS-XE, define their available resources and the API calls to manage them

### How Terraform Works

- Code: Admin creates the config files
- Plan: Terraform checks the differences between the current state in the state file and the desired state in the config files, then determines the necessary actions to apply. Admin checks the actions
- Apply: The actions are executed
- Consolidate: The state file is updated

## Configuration Management Tool Support

Ansible, Puppet, Chef and Terraform were designed primarily for server system administration
Ansible and Terraform are more suitable for network environments than Puppet and Chef because they do not require agents
There is limited support on Cisco devices to run agents

## Ansible vs Terraform

- Terraforms primary focus is an infrastructure provisioning tool
- It uses a declarative approach where a desired state is defines and the tool takes actions to achieve it
- It is lifecycle aware

- Ansible's primary focus is as a config tool
- It uses procedural approach with a granular sequence of steps that are followed to reach the desired end result
- Not lifecycle aware

Ansible and Terraform can be used together, for example:
Use Terraform to provision infrastructure then call Ansible to push configs to the resources. Use Ansible for future config changes
### Ansible vs Terraform: Mutable vs Immutable

Ansible objects are considered mutable, Terraform immutable by default

COMMAND LINE WILL OVERWRITE

# Software Defined Network

## Router and Switch Planes

- Data (Forwarding Plane): Traffic which is forwarded through the device
- Control Plane: Makes decisions about how to forward traffic. Control plane packets such as routing protocols or spanning tree updates are destined to or locally originated from the devices itself
- Management Plane: Device is configured and monitored in the management plane. For example at the CLI through Telnet or SSH via a GUI using HTTPS, or via SNMP or an API

## SDN - Data and Control Plane Separation

- Network infrastructure devices are responsible for their own individual control and data planes in a traditional environment
- SDN decouples the data and control planes; infrastructure devices are still responsible for forwarding traffic but the control plan moves to a centralized SDN controller

## Data and Control Plane Separation

- Rules for packet handling are sent to the network infrastructure devices from the controller
- The network infrastructure devices query the controller for guidance as needed, and provide it with information about traffic they are handling

## Pure SDN vs Hybrid SDN

- Pure SDN - the control plane runs purely on as SDN controller, and the data plane runs purely on the network devices
- Hybrid SDN - the majority of the control plane intelligence is provided by an SDN controller, but the network devices retain some control plane intelligence as well as the data plane operation

## SDN Architecture

On CCNA, everything is from the POV of the SDN controller

![[attachments/Pasted image 20260316194830.png]]

## Cisco SDN Controllers APIC

Application Policy Infrastructure Controller
Designed to manage data center environments with Nexus switches

# Catalyst Center

## Intent Based Networking (IBN)

- IBN builds on software defined networking to move away from a network of individual devices which are manually managed one by one to a controller-lead network that is managed as an integrated whole
- It captures business intent and translates it into policies that can be automated and applied consistently across the network 
- It continuously  monitors and adjusts network performance to help assure desired business outcomes
## Cisco Software Defined Architecture

- Catalyst Center
- SD-Access
- SD-WAN
## Catalyst Center

- Catalyst Center is a Cisco SDN controller which is designed to manage enterprise environments - campus, branch, WAN (As opposed to the APIC which manages data center environments with Nexus switches)
- It runs as a virtual appliance in the cloud or on-prem, or as a physical appliance on Cisco UCS server hardware
- Underlying operation system is Linux
- Can be clustered for redundancy
## IBN Example

Example 1: a QoS policy roll-out
The Intent: The network policy is first defined, for example providing guaranteed service to voice and video across network locations

- The network team creates an Application Policy in Catalyst Center specifying voice and video as business relevant applications.
- Catalyst Center automatically configures the best practice QoS settings on the network devices.
- This can reduce total deployment time from months to minutes
## Network Plug and Play

- Allows router, switches, and wireless APs to be deployed in remote offices with zero touch configuration
- The device is physically installed on the remote office and connected to the network
- It discovers Catalysts Center through various methods such as DHCP option 43 or DNS 'pnpserver.domain-name.com'
- It then registers with and downloads its configuration from Catalyst Center
- This ensures consistent configuration of remote office devices with no need for a network engineer on site

## Assurance

Makes sure your devices are doing what they need to do

### Peer Comparison

Compares wireless network quality with comparable size peer networks

# SD-Access Software

SD-Access is a newer method of network access control which solves the limitation of the traditional implementation
Traffic flow security is based on user identity, not physical location and IP address
Users log in from and can move to any physical location in the network

Two components required for SD-Access:
- Uses are authenticated by the ISE
- The security policy (permitted and denied communication between groups) is configured on the Catalyst Center

## Underlay and Overlay Network

- An underlay network is the underlying physical network. It provides the underlying physical connections which the overlay network is built on top of
- An overlay network is the logical topology used to virtually connect devices. It is built over the physical underlay network
- The combination of the two is known as the network fabric

## Underlay Network

- When SD-Access is plugged into an existing network ('brownfield') , any configuration can be used for the underlying physical network. Link between devices can be layer 2 or 4 and any routing protocol can be used
- Catalyst Center can be used to automatically provision underlay networks in new ('greenfield') sites. In this case, layer 3 links are used between devices and IS-IS is used as the routing protocol

## Overlay Network

- LISP is used for the Control Plane - has information of where devices are on a network
- VXLAN is used for the Data Plane - will be built to connect the devices together once info is received from LISP of where the devices are located
- Cisco TrustSec CTS is used for the policy

## Cisco TrustSec CTS

Users are authenticated through ISE
Security policy is configured on Catalyst Center
Users are allocated Scalable Group Tags (SGT)
Cisco TrustSec secures traffic flows based on the security policy and SGTs

# SD-WAN

Cisco acquired Viptela to enhance their WAN solution
Provides automated setup of WAN connectivity between sites
Monitoring and failover is automated
Traffic flow is application aware

## SD-WAN Benefits

- Automated, standardized setup of connectivity between sites
- Transport independent
- More flexibility and easier to migrate WAN services
- The required, predictable performance for important applications
- Integration with the latest cloud and network technologies
- Lower cost

## SD WAN Architecture

![[attachments/Pasted image 20260316221339.png]]
## Data Plane -WAN Edge Routers

- WAN Edge routers (vEdge) run the data plane
- They are physical or virtual routers
- They form an IPsec encrypted data plane between each other
- A site can have two WAN routers for redundancy

## Control Plane - SD WAN Controllers

- SD-WAN controllers run the control plane
- They are the centralized brain of the solution
- They run as virtual machines
- They distribute policy and forwarding information to the WAN edge routers inside TLS tunnels
- Each WAN edge router connects to two SD-WAN controllers for redundancy

## Management Plane - SD WAN Manager

- SD-WAN Manager (aka the vManage NMS) provides the management plane GUI.
- It enables centralized configuration and simplifies changes.
- It provides real time alerting.
- It runs as a virtual machine.
- Multiple SD-WAN Managers are clustered for redundancy.

## Orchestration - SD WAN Validator

- The SD-WAN Validator (aka vBond orchestrator) authenticates all SD-WAN Controllers, SD-WAN Managers and WAN Edge routers that join the SD-WAN network.
- It enables WAN Edge routers to discover each other as well as SD-WAN Managers and SD-WAN Controllers.
- It has a public IP address and is deployed in the DMZ.
- It runs as a virtual machine (can also run on a router in smaller deployments.)
- Multiple SD-WAN Validator orchestrators can be deployed with round robin DNS

## Zero Touch Provisioning (ZTP) 

- Cloud based shared service hosted by Cisco
- Utilized on first boot of WAN Edge router only
- Directs WAN Edge to SD-WAN Validator to orchestrate joining it to the network

## BF VPN Tunnel Monitoring

Bidirectional Forwarding Detection packets are sent over all VPN tunnels
This detects if a tunnel goes down and also provides latency, jitter, and loss statistics

## Traffic Forwarding Options

If multiple tunnels are available traffic can be load balanced over the tunnels:
Active/Active
Weighted Active/Active
Application pinning Active/Standby
Application Aware Routing

## Application Aware Routing

- BFD monitors latency, jitter, and loss across the VPN
- Can set minimum requirements for an application wit SLA Classes
- SD-WAN ensures the application is sent over a link which meets its SLA requirements

# Cisco Meraki

Provides secure cloud managed networking
This is through the Meraki Dashboard
Reduces costs
Scalable to hundreds of thousands of devices

## Simplified Deployment and Configuration

- When Meraki devices are powered on they automatically connect to the Meraki cloud over the internet. 
- Zero Touch Deployment allows devices to be configured before they are connected. When the device is installed later it connects to the Meraki Cloud and downloads its configuration.
- Configuration templates can be created and updates automatically pushed to devices
## References
