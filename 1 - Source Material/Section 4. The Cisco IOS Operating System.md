
32025-08-08 18:00
Status:
Flashcards:
Source: [[]]
Tags: [[../2 - Tags/Cisco OS|Cisco OS]]


Interconnection Operating System
# Cisco Operating System

# Connecting to a Cisco Device Over the Network

To get to the CLI of a Cisco device, you will use SSH to connect to it's management IP address over the network. Telnet is supported but not recommended

In enterprise networks, secure login will typically be enforced with centralized AAA (Authentication, Authorization, and Accounting) server that's got access to the central database of all your usernames and passwords instead of having them on each separate device.

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
Router# ;; Privilege Exec mode (<span style="color:rgb(255, 192, 0)">enable</span>)
hostname(config)#  ;; Global Configuration mode (<span style="color:rgb(255, 192, 0)">conf t</span>) (Configure Terminal)
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

iOS has tab completion

\<cr> means there are optional keywords, not necessarily needed 

<span style="color:rgb(255, 192, 0)">show</span> command gives you point in time information, <span style="color:rgb(255, 192, 0)">debug</span> updates in real time

# Navigating the Cisco IOS Operating System Part 2

Ctrl-A moves cursor to the beginning of the line
Ctrl-U deletes the whole line

Entering commands at the wrong level will happen a lot as a beginner. **Show and debug function at privilege exec mode**. Entering <mark style="background: #D2B3FFA6;">do</mark> before a show command in any mode (except privilege exec mode) will run this command

<span style="color:rgb(255, 192, 0)">exit</span> ;; drops down a level

You must progress through each level one by one, you can't skip levels

Most common iOS command
- show ip interface brief
- show running-config
# Cisco Configuration Management

- In iOS, whenever you make a change, the change takes effect immediately. The change goes into the running configuration. 
- Startup configurations take effect when the router is started again
- <span style="color:rgb(255, 192, 0)">copy run start</span> to apply running config to startup config
- You can backup running config by typing in <span style="color:rgb(255, 192, 0)">copy run ?</span> and it will give you various locations to save the file. Must give file a name.
- If you want to restore from a back up, you'll do this by copying to the startup configuration and then rebooting.  However, copy merges commands instead of replacing so we use <span style="color:rgb(255, 192, 0)">erase start</span> first and then copy the file  you wish to restore from. 
	Ex. copy flash:my-config start

- <span style="color:rgb(255, 192, 0)">copy run tftp </span> backs up to TFTP server
- use <span style="color:rgb(255, 192, 0)">more</span> to see content of back up file

### Config Storage Locations

- IOS image is store on Flash
- Startup config is stored on NVRAM
- The running config is stored RAM (Loaded into RAM from the startup config when the device boots up )