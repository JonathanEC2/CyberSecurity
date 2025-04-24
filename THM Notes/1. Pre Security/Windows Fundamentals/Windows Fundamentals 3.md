# Windows Fundamentals 3

## Windows Updates
Windows Update is a service provided by Microsoft to provide security updates, feature enhancements, and patches for the Windows operating system and other Microsoft products, such as Microsoft Defender. 

## Windows Security 
Windows Security is your home to manage the tools that protect your device and your data

## Virus and Threat Protection

Current threats scan options:
- Quick scan - Checks folders in your system where threats are commonly found.
- Full scan - Checks all files and running programs on your hard disk. This scan could take longer than one hour.
- Custom scan - Choose which files and locations you want to check.

## Virus & threat protection settings 

- Real-time protection - Locates and stops malware from installing or running on your device.
- Cloud-delivered protection - Provides increased and faster protection with access to the latest protection data in the cloud.
- Automatic sample submission - Send sample files to Microsoft to help protect you and others from potential threats. 
- Controlled folder access - Protect files, folders, and memory areas on your device from unauthorized changes by unfriendly applications.
- Exclusions - Windows Defender Antivirus won't scan items that you've excluded.
- Notifications - Windows Defender Antivirus will send notifications with critical information about the health and security of your device. 

 ## [Firewall & network protection](https://learn.microsoft.com/en-us/windows/security/operating-system-security/network-security/windows-firewall/configure)

- Domain - The domain profile applies to networks where the host system can authenticate to a domain controller. 
- Private - The private profile is user-assigned and is used to designate private or home networks.
- Public - The default profile is the public profile, used to designate public networks such as Wi-Fi hotspots at coffee shops, airports, and other locations.

  
## App & browser control
Windows Defender SmartScreen helps protect your device by checking for unrecognized apps and files from the web. 
## Device security
Memory Integrity - Prevents attacks from inserting malicious code into high-security processes.

Trusted Platform Module (TPM) technology is designed to provide hardware-based, security-related functions. A TPM chip is a secure crypto-processor that is designed to carry out cryptographic operations. The chip includes multiple physical security mechanisms to make it tamper-resistant, and malicious software is unable to tamper with the security functions of the TPM".

## BitLocker 
BitLocker Drive Encryption is a data protection feature that integrates with the operating system and addresses the threats of data theft or exposure from lost, stolen, or inappropriately decommissioned computers

## Volume Shadow Copy Service
 Volume Shadow Copy Service (VSS) coordinates the required actions to create a consistent shadow copy (also known as a snapshot or a point-in-time copy) of the data that is to be backed up.  Malware writers know of this Windows feature and write code in their malware to look for these files and delete them. Doing so makes it impossible to recover from a ransomware attack unless you have an offline/off-site backup.

  
To learn more about the Windows OS, you'll need to continue the journey on your own
Further reading material:


 [https://docs.microsoft.com/](https://docs.microsoft.com/)
 
[https://learn.microsoft.com/](https://learn.microsoft.com/)

[Antimalware Scan Interface](https://learn.microsoft.com/en-us/windows/win32/amsi/antimalware-scan-interface-portal)

[Credential Guard](https://learn.microsoft.com/en-us/windows/security/identity-protection/credential-guard/configure?tabs=intune)

[Windows 10 Hello](https://support.microsoft.com/en-us/windows/learn-about-windows-hello-and-set-it-up-dae28983-8242-bb2a-d3d1-87c9d265a5f0#:~:text=Windows%2010,in%20with%20just%20your%20PIN.)

[CSO Online - The best new Windows 10 security features](https://www.csoonline.com/article/564531/the-best-new-windows-10-security-features.html)