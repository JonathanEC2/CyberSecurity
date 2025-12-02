[[../2 - Tags/Windows]]

## The File System

The file system used in modern versions of Windows is the New Technology File System or simply NTFS. Before NTFS, there was FAT16/FAT32 (File Allocation Table) and HPFS (High Performance File System). NTFS is known as a journaling file system. In case of a failure, the file system can automatically repair the folders/files on disk using information stored in a log file.


You can set permissions on NTFS volumes that grant or deny access to files and folders. The permissions are:

- Full control
- Modify
- Read & Execute
- List folder contents
- Read
- Write

View the permissions for a file or folder Right Click File Or <span style="color:rgb(0, 176, 80)">Folder > Properties > Security</span>

Another feature of NTFS is Alternate Data Streams (ADS). Alternate Data Streams (ADS) is a file attribute specific to Windows NTFS (New Technology File System). Every file has at least one data stream ($DATA), and ADS allows files to contain more than one data stream.

## The Windows\System32 Folders

Environment variables store information about the operating system environment. This information includes details such as the operating system path, the number of processors used by the operating system, and the location of temporary folders. The environment variable for the Windows directory is <span style="color:rgb(0, 176, 240)">%windir%</span>. The System32 folder holds important files that are critical for the operating system. You should proceed with extreme caution when interacting with this folder. Accidentally deleting any files or folders within System32 can render the Windows OS inoperational.

## User Accounts, Profiles, and Permissions

Local User and Group Management. Right-click on the Start Menu and click Run. Type <span style="color:rgb(255, 192, 0)">lusrmgr.msc</span>


## User Account Control

Elevated privilege increases the risk of system compromise because it makes it easier for malware to infect the system. Consequently, since the user account can make changes to the system, the malware would run in the context of the logged-in user. To protect the local user with such privileges, Microsoft introduced **User Account Control (UAC)**. UAC works when a user with an account type of administrator logs into a system, the current session doesn't run with elevated permissions. When an operation requiring higher-level privileges needs to execute, the user will be prompted to confirm if they permit the operation to run. 