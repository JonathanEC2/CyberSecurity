Interconnection Operating System
# Cisco Operating System

# Connecting to a Cisco Device Over the Network

To get to the CLI of a Cisco device, you will use SSH to connect to it's management IP address over the network. Telnet is supported but not recommended

In enterprise networks, secure login will typically be enforced with centralized AAA (Authentication, Authorization, and Accounting) server

## Out of Band Management

Production network is the network that is being used for your normal user traffic

Large companies will also have a management network as well. By having a dedicated management network, it gives you a back up path to connect to network devices if there is an issue with the connection of the production network. 

Connection to Production network = in band
Connection to Management network = out of band
# Making the Initial Connection to a Cisco Device

Cisco devices usually don't have a default IP address, so one needs to be set up before we can connect to it. 

We need a way to connect to the device to do the initial configuration. This is done using **console connection**

## Console Cable (USB to USB Mini)

Gives you low level direct access to the command line. 

- In Putty, select serial port to begin configuration
- Navigate to device manager and select ports to see the name of Comm Port
- Power on router

## Console Connection Troubleshooting

As well as initial configuration, the console port is also useful when the devices IP address becomes unresponsive. It can also be used to troubleshoot the boot up process. This is unavailable with SSH because SSH needs IP address to be able to connect, but it will not be live during boot up.

# Navigating the Cisco IOS Operating System Part 1

Router> ;;User Exec Mode
Router# ;; Privilege Exec mode (<span style="color:rgb(255, 192, 0)">Enable</span>)
hostname(config)#  ;; Global Configuration mode (<span style="color:rgb(255, 192, 0)">Configuration terminal</span>)
hostname(config-if)# ;; Interface Configuration mode (<span style="color:rgb(255, 192, 0)">I<span style="color:rgb(255, 192, 0)">nter</span>face x</span>)


<span style="color:rgb(255, 192, 0)">enable</span> ;; to enter privilege exec mode
<span style="color:rgb(255, 192, 0)">disable</span> ;; to return to user exec mode
<span style="color:rgb(255, 192, 0)">end</span> ;; drops to Privilege Exec mode from any level
<span style="color:rgb(255, 192, 0)">show</span> ;; displays information about the router. Gives point in time information 
<span style="color:rgb(255, 192, 0)">debug</span> ;; output will be updated in real time 
<span style="color:rgb(255, 192, 0)">?</span> access Help
	sh? will show all commands that start with sh
	show ? will show all available keyword options for 'show'

Abbreviated commands must be ambiguous, there must only be one possible match for what you types for the abbreviation to succeed

Has tab completion

# Navigating the Cisco IOS Operating System Part 2



# Cisco Configuration Management

