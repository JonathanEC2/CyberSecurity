[[../2 - Tags/Windows|Windows]]
## System Configuration
 **System Configuration**;; utility (<span style="color:rgb(255, 192, 0)">MSConfig</span>) is for advanced troubleshooting, and its main purpose is to help diagnose startup issues. 

1. General -  select what devices and services for Windows to load upon boot
2. Boot -  various boot options for the Operating System
3. Services - lists all services configured for the system regardless of their state
4. Startup - items that start on boot
5. Tools - various utilities to configure the operating system further. There is a brief description of each tool to provide some insight into what the tool is for. 

[Task Manager](https://www.howtogeek.com/405806/windows-task-manager-the-complete-guide/)
## Computer Management

Computer Management;; (<span style="color:rgb(255, 192, 0)">compmgmt</span>) utility has three primary sections: System Tools, Storage, and Services and Applications.
#### System Tools

- **Task Scheduler** can create and manage common tasks that our computer will carry out automatically at the times we specify.
- **Event Viewer** allows us to view events that have occurred on the computer. These records of events can be seen as an audit trail that can be used to understand the activity of the computer system. This information is often used to diagnose problems and investigate actions executed on the system. 
	- Five types of events can be logged. This is a [table](https://learn.microsoft.com/en-us/windows/win32/eventlog/event-types) providing a brief description of each.
	- The standard logs are visible under Windows Logs. This is a [table](https://learn.microsoft.com/en-us/windows/win32/eventlog/eventlog-key) providing a brief description of each.
- **Shared Folders** is where you will see a complete list of shares and folders shared that others can connect to. 
- **Local Users** and Groups lusrmgr.msc
- In **Performance**, you'll see a utility called Performance Monitor (perfmon). Perfmon is used to view performance data in real-time or from a log file. This utility is useful for troubleshooting performance issues on a computer system, whether local or remote. 
- **Device Manager** allows us to view and configure the hardware, such as disabling any hardware attached to the computer.

#### Storage
- Under Storage is Windows Server Backup and Disk Management. Disk Management is a system utility in Windows that enables you to perform advanced storage tasks.  Some tasks are:
	- Set up a new drive
	- Extend a partition
	- Shrink a partition
	- Assign or change a drive letter (ex. E:) 

#### Services and Applications
- Services and Applications. WMI Control configures and controls the Windows Management Instrumentation (WMI) service. WMI allows scripting languages (such as VBScript or Windows PowerShell) to manage Microsoft Windows personal computers and servers, both locally and remotely. Microsoft also provides a command-line interface to WMI called Windows Management Instrumentation Command-line (WMIC)

## System Information

This tool gathers information about your computer and displays a comprehensive view of your hardware, system components, and software environment, which you can use to diagnose computer issues.

-  [Hardware Resources](https://learn.microsoft.com/en-us/windows-hardware/drivers/kernel/hardware-resources) is not for the average computer user. 
- Under Components, you can see specific information about the hardware devices installed on the computer.
- In the Software Environment section, you can see information about software baked into the operating system and software you have installed. Other details are visible in this section as well, such as the Environment Variables (See Windows Fundamentals 1)  

## Resource Monitor

Resource Monitor displays per-process and aggregate CPU, memory, disk, and network usage information, in addition to providing details about which processes are using individual file handles and modules. Advanced filtering allows users to isolate the data related to one or more processes (either applications or services), start, stop, pause, and resume services, and close unresponsive applications from the user interface.  This utility is geared primarily to advanced users who need to perform advanced troubleshooting on the computer system.

## Command Prompt 

- <span style="color:rgb(255, 192, 0)">hostname</span> will output the computer name.
- <span style="color:rgb(255, 192, 0)">whoami</span> will output the name of the logged-in user.
- <span style="color:rgb(255, 192, 0)"><span style="color:rgb(255, 192, 0)"> ipconfig</span></span>  will show the network address settings for the computer.
- <span style="color:rgb(255, 192, 0)"> /?</span>  to retrieve the help manual for a command.
- <span style="color:rgb(255, 192, 0)">Cls</span> To clear the command prompt screen.
- <span style="color:rgb(255, 192, 0)">Netstat</span> will display protocol statistics and current TCP/IP network connections.
- <span style="color:rgb(255, 192, 0)">net</span> command is primarily used to manage network resources.

## Windows Registry

 Windows Registry  (per Microsoft) is a central hierarchical database used to store information necessary to configure the system for one or more users, applications, and hardware devices.
 
The registry contains information that Windows continually references during operation, such as:
- Profiles for each user
- Applications installed on the computer and the types of documents that each can create
- Property sheet settings for folders and application icons
- What hardware exists on the system
- The ports that are being used.
 
The registry is for advanced computer users. Making changes to the registry can affect normal computer operations. 
