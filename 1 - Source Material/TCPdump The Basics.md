

#tcp_dump
Tcpdump tool and its libpcap library are written in C and C++

## Basic Packet Capture

- <span style="color:rgb(255, 192, 0)">-i</span> ;; specifies interface could use <span style="color:rgb(0, 176, 240)">any</span> to listen on all interface or specify one such as <span style="color:rgb(0, 176, 240)">eth0</span>
<!--SR:!2025-01-09,3,250-->
- <span style="color:rgb(255, 192, 0)">ip address show</span> (<span style="color:rgb(255, 192, 0)">ip a s </span>) ;; lists available network interfaces
<!--SR:!2025-01-09,2,230-->
- <span style="color:rgb(255, 192, 0)">-w FILE</span> ;; saves captured packets
<!--SR:!2025-01-08,1,210-->
- <span style="color:rgb(255, 192, 0)">-r FILE</span> ;; reads captured packets.  You can capture network traffic over a suitable time frame to inspect a protocol, then read the captured packets while applying filters to display the packets you are interested in
<!--SR:!2025-01-09,2,230-->
- <span style="color:rgb(255, 192, 0)">-c COUNT</span> ;; specifies number of packets to capture
<!--SR:!2025-01-09,2,230-->
- <span style="color:rgb(255, 192, 0)">-n</span> ;; avoids making DNS lookups
<!--SR:!2025-01-09,3,250-->
- <span style="color:rgb(255, 192, 0)">-nn</span> ;; stops both DNS and port number lookups
<!--SR:!2025-01-08,1,210-->
- <span style="color:rgb(255, 192, 0)">- v</span> ;; verbose output. add up to three v's for more verbose output
<!--SR:!2025-01-10,4,270-->

## Filtering Expressions

<u><b>Filtering by Host</b></u>
<span style="color:rgb(255, 192, 0)">src host IP</span> or <span style="color:rgb(255, 192, 0)">HOSTNAME</span>  ;; limits packets from a particular source IP address or hostname
<!--SR:!2025-01-09,3,250-->
<span style="color:rgb(255, 192, 0)">dst host IP</span> or <span style="color:rgb(255, 192, 0)">HOSTNAME</span> ;; limit packets sent to a specific destination
<!--SR:!2025-01-09,2,230-->

<u><b>Filtering by Port</b></u>
<span style="color:rgb(255, 192, 0)">port</span> ;; specifies port
<!--SR:!2025-01-10,4,270-->
<span style="color:rgb(255, 192, 0)">scr</span> or <span style="color:rgb(255, 192, 0)">dst</span> <span style="color:rgb(255, 192, 0)">PORT_NUMBER</span> ;; packets sent to or from a specific port number.
<!--SR:!2025-01-10,4,270-->

<u><b>Filtering by Protocol</b></u>
<span style="color:rgb(255, 192, 0)">ip</span>, <span style="color:rgb(255, 192, 0)">ip6</span>, <span style="color:rgb(255, 192, 0)">udp</span>, <span style="color:rgb(255, 192, 0)">tcp</span>, and <span style="color:rgb(255, 192, 0)">icmp</span> ;; filter by protocol
<!--SR:!2025-01-10,4,270-->

<u><b>Logical Operators</b></u>
<span style="color:rgb(255, 192, 0)">and</span> ;; captures traffic when both conditions are true
<!--SR:!2025-01-10,4,270-->
<span style="color:rgb(255, 192, 0)">or</span> ;; captures traffic when one of the conditions are true
<!--SR:!2025-01-10,4,270-->
<span style="color:rgb(255, 192, 0)">not</span> ;; captures traffic when the condition is not true
<!--SR:!2025-01-10,4,270-->

<span style="color:rgb(255, 192, 0)">wc </span> you can count the lines by piping the output
## Advanced Filtering

<span style="color:rgb(255, 192, 0)">greater LENGTH</span> ;; filters packets that have a length greater than or equal to the specified length
<!--SR:!2025-01-10,4,270-->
<span style="color:rgb(255, 192, 0)"> less LENGTH </span>;; filters packets that have a length less than or equal to the specified length
<!--SR:!2025-01-09,3,250-->

<span style="color:rgb(255, 0, 0)">man pcap-filter</span> 

<b><u> Binary Operations</u></b>

<span style="color:rgb(255, 192, 0)">&</span> (And) takes two bits and returns 0 unless both inputs are 1, as shown in the table below.

|Input 1|Input 2|Input1 `&` Input 2|
|---|---|---|
|0|0|0|
|0|1|0|
|1|0|0|
|1|1|1|

<span style="color:rgb(255, 192, 0)">|</span> (Or) takes two bits and returns 1 unless both inputs are 0. This is shown in the table below.

|Input 1|Input 2|Input 1 `\|` Input 2|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|1|

<span style="color:rgb(255, 192, 0)">!</span> (Not) takes one bit and inverts it; an input of 1 gives 0, and an input of 0 gives 1, as shown in the table below.

|Input 1|`!` Input 1|
|---|---|
|0|1|
|1|0|

<b><u> Header Bytes</u></b>

Filter packets based on content of a header byte using the syntax <span style="color:rgb(255, 192, 0)">proto[expr:size]</span> where:
- <span style="color:rgb(255, 192, 0)">proto</span> ;; refers to the protocol such as arp, ether, icmp, ip, ip6, tcp, and udp
<!--SR:!2025-01-10,4,270-->
- <span style="color:rgb(255, 192, 0)">expr</span> ;;indicates the byte offset, where 0 refers to the first byte
<!--SR:!2025-01-08,1,210-->
- <span style="color:rgb(255, 192, 0)">size</span> ;; indicates the number of bytes that interest us
<!--SR:!2025-01-09,2,230-->

You can use <span style="color:rgb(255, 192, 0)">tcp[tcpflags]</span> to refer to the TCP flags field. The following TCP flags are available to compare with:

tcp-syn TCP SYN (Synchronize)
tcp-ack TCP ACK (Acknowledge)
tcp-fin TCP FIN (Finish)
tcp-rst TCP RST (Reset)
tcp-push TCP Push

## Displaying Packets

<span style="color:rgb(255, 192, 0)">-q</span> ;; Quick output; print brief packet information
<!--SR:!2025-01-08,1,210-->
<span style="color:rgb(255, 192, 0)">-e</span> ;; Print the link-level header
<!--SR:!2025-01-08,1,210-->
<span style="color:rgb(255, 192, 0)">-A</span> ;;Show packet data in ASCII
<!--SR:!2025-01-08,1,210-->
<span style="color:rgb(255, 192, 0)">-x</span> ;; Show packet data in hexadecimal format, referred to as hex
<!--SR:!2025-01-08,1,210-->
<span style="color:rgb(255, 192, 0)">-X</span> ;; Show packet headers and data in hex and ASCII
<!--SR:!2025-01-08,1,210-->

