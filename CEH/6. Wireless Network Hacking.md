#wirelessnethacking
# Wireless Network Hacking
WPA3 Personal;; uses SAE
WPA3 Enterprise;; uses AES-GCMP
WPA2 Personal;; uses AES CCMP
WPA2 Enterprise;; uses 802.1
WEP;; 24-bit IV using RC4

# Attacks
Key Reinstallation Attack (KRACK);;  a replay attack exploiting WPA2 for way handshake
KoreK chop;; decrypts <span style="color:rgb(255, 0, 0)">WEP</span> packets without requiring the key
Wardriving;; search for wireless APs
Aircrack-ng;; tool for cracking WEP, WPA, and WPA2 does not use rainbow tables to crack WEP keys
	dictionary for WPA2 keys
	PTW against WEP

## Tools
### aLTEr
aLTEr active how attacker simulates a legit cell tower using redirect connections
aLTEr passive eavesdrops instead of manipulating packets and redirecting users
aLTEr identity mapping how attacker <span style="color:rgb(255, 0, 0)">matches volatile radio identities</span> to longer lasting ones
aLTEr website <span style="color:rgb(255, 0, 0)">fingerprinting</span> how attacker uses Layer 2 meta-info to determine which site a user visits


![[Pasted image 20240814124732.png]]