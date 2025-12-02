
# Scanning
- Network-based;; runs from dedicated hosts, such as an appliance or VM. can effectively scan and device in IP range such as IoT or OT
- Agent-based;; installation of a small amount of code on each system. can be performed locally and provide greater detail that net-based. can scan while host is offline
- Credentialed;; access significantly more, better intel
- noncredentialled;; less disruptive 

- hitlist scanning;; contains a list of targets likely to be vulnerable to the malware
- topological scan;; uses info gathered from infected host to target addition host
- permutation scanning;; modifies the divide and conquer method to mitigate detection by IDSs



# Passwords Attacks

- brute force;; tries every combination of letters, numbers, and symbols to discover spassword. Typically takes the longest
- dictionary;; compares list of passwords against a list of words
- hybrid;; checks password list against a list of words but replaces some letters with numbers or symbols

THC hydra;; uses dictionary lists and hybrid brute-force methods
Rainbowcrack;; rainbow table
OphCrack;; rainbow table
Cain and able;; rainbow table

# Buffer overflow
fgets function in C library performs bounds checking
# Assessment solutions
- service-based;; mimics perspective of malicious actor, multiple vendors
- product-based;; centered around locally installed vulnerability assessment technologies from a single vendor. Managed by org staff and can require significant resources to keep up to date
- tree-based;; uses list of vulnerabilities to determine what tests to run. may run tests that are not applicable to the system and produce high false positives
- inference-based;; begin with intel gathering phase that learns about target system. launches attack based on info gathered. reduced false positives

- Passive vulnerability assessment is vulnerability scanning
- Active vulnerability assessment assessment is penetration testing
# Other

- Advanced Malware Protection
	- Disposition field status - if uploaded would say <span style="color:rgb(255, 0, 0)">unknown</span> or malicious
	- upload_action field would contain a <span style="color:rgb(255, 0, 0)">1</span>
	- Info field indicated output was received from <span style="color:rgb(255, 0, 0)">cache</span> not <span style="color:rgb(255, 0, 0)">cloud</span>

hypervisor rootkit migrates the OS into VM
kernel rootkit
app rootkit
library rootkit infects DLL


- Domain Generation Algorithm (DGA);; exploits nature of reputation-based security systems. ensures attackers C2 systems remain accessible. Relies on domains that have not been categorized by reputation-based systems

- Signature definition files;; used to update security software
- MEDUSA a tool that can be used to gather OSINT data from social media platforms
- Hootsuite a social media management platform
- CVSS 3.1 0.0;; none
- NTPv3 provides encryption, authentication, and integrity
- Phishing;; attempts to get users to reveal PII
- Fileless malware;; uses evasion that prevents it from being detected by typical antivirus solutions

DNS fast fluxing;; a technique that involves associating multiple IP addresses with a single domain name and changing out these IP addresses rapidly.
<span style="color:rgb(255, 0, 0)">Doublefluxing</span> ;; is similar to fastfluxing but relies on separate botnet to proxy DNS services for the attacker

- stealth virus;; intercepts calls made to OS
- Sparse infector virus;; infect files only when conditions are met
## msfvenom

msfvenom -f;; format
msfvenom -a;; architecture such as x86
msfvenom -b;; bad characters that should not be included in shell code. -b \x00 ensures null bytes will not be included


### APT lifecycle
1. preparation
2. initial intrusion - malware
3. expansion- get admin access or spread malware
4. persistence - create addition footholds such as C2 hosts
5. search and exfiltration - finally gains access to targeted resource
6. cleanup
