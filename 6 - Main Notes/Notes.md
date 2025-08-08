## Network Settings

- NAT - Creates separate network using the host adapter and will assign it to each VM; each VM will have its own network
- NAT Network - All machines will mesh into one network
- Bridged - will act as physical machines, it'll be on the same network as your host machine. <span style="color:rgb(255, 0, 0)"><u><b>DONT EXECUTE MALWARE IN THIS MODE!</u></b></span> 
- Host only - only accessible to the host machine, no internet access or LAN
- Internal network - puts VMs in their own network, <span style="color:rgb(0, 176, 80)">use when executing malware</span>. Custom assign IPs and no Internet access
	- change adapter options > Ethernet > Properties > IPv4
	- Custom IP address: 192.168.20.10 and 192.168.20.11
	- subnet: /24

select not attached if running malware

![[Pasted image 20241101121252.png]]
https://www.youtube.com/watch?v=5iafC6vj7kM&t=25s

