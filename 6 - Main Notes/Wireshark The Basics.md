
## Tool Overview

Wireshark can be used to:
- Detect and troubleshoot network problems such as congestion
- Detect security anomalies, such as rogue hosts and abnormal port usage
- Investigate and learn protocol details, such as response code and payload data

<u><b>Coloring Packets</b></u>
<span style="font-weight:bold; color:rgb(0, 176, 80)">View --> Coloring Rules</span> menu to create permanent coloring rules
<span style="color:rgb(0, 176, 80)">View --> Conversation Filter</span> temporary packet coloring

 <u><b>Merge PCAP Files</b></u>
<span style="color:rgb(0, 176, 80)">File --> Merge</span> 

<u><b>View File Details   </b></u>
<span style="color:rgb(0, 176, 80)">Statistics --> Capture File</span> Properties shows file hash, capture time, capture file comments, interface and statistics
## Packet Dissection

Investigates packets by decoding available protocols and fields

- The Frame (Layer 1):  shows  what frame/packet you are looking at and details specific to the **Physical** layer of the OSI model
- Source (MAC) (Layer 2): Shows source and destination MAC addresses; from **Data Link** layer
- Source (IP) (Layer 3): Source and destination IPv4 addresses; from **Network** layer of OSI model
- Protocol (Layer 4): show  details of the protocol used (UDP/TCP) and source and destination ports; from the Transport layer of the OSI model.
	- Protocol **errors**: shows specific segments from TCP that needed to be reassembled
- Application Protocol (Layer 5): shows details specific to the protocol used, such as HTTP, FTP,  and SMB. From the **Application** layer of the OSI model.
	- Application data: shows application-specific data

## Packet Navigation

 <u><b>Find Packets</b></u>
<span style="color:rgb(0, 176, 80)">Edit --> Find Packet </span>to search inside a packet for a particular event of interest

There are two crucial points in finding packets:
 - **Input type**: This functionality accepts four types of inputs (Display filter, Hex, String and Regex)
 - **Search field**:  You can conduct searches in the three panes (packet list, packet details, and packet bytes). It is important to know the available information in each pane

  <u><b>Mark Packets</b></u>
You can find/point to a specific packet for further investigation by marking it. Use <span style="color:rgb(0, 176, 80)">edit</span> or <span style="color:rgb(0, 176, 80)">right click</span> to mark

<mark style="background: #FFF3A3A6;">Marked packets will be lost after closing the capture file</mark>

   <u><b>Packet Comments</b></u>
Similar to packet marking except comments stay after closing file

<u><b>Export Packets</b></u>
Sometimes it is necessary to separate specific packages from the file and dig deeper to resolve an incident. You can use the <span style="color:rgb(0, 176, 80)">File</span> menu to export packets.

<u><b>Export Objects (Files) </b></u>
Wireshark can extract files transferred through the wire. For a security analyst, it is vital to discover shared files and save them for further investigation.

 <u><b>Time Display Format</b></u>
<span style="color:rgb(0, 176, 80)">View --> Time Display Format</span>  to change the time display format

<u><b>Expert Info  </b></u>
<span style="color:rgb(0, 176, 80)">Analyse --> Expert Information</span>

 Wireshark can detect specific states of protocols to help analysts easily spot anomalies and problems. They are only suggestions and there is always a chance of having false positive/negatives

| **Severity** | **Colour**                                             | **Info**                                                 |
| ------------ | ------------------------------------------------------ | -------------------------------------------------------- |
| **Chat**     | **<span style="color:rgb(15, 53, 240)">Blue</span>**   | Information on usual workflow.                           |
| **Note**     | **<span style="color:rgb(0, 176, 240)">Cyan</span>**   | Notable events like application error codes.             |
| **Warn**     | **<span style="color:rgb(255, 255, 0)">Yellow</span>** | Warnings like unusual error codes or problem statements. |
| **Error**    | **<span style="color:rgb(255, 0, 0)">Red</span>**      | Problems like malformed packets.                         |


Go to packet number 39765
Look at the "packet details pane". Right-click on the JPEG section and "Export packet bytes". This is an alternative way of extracting data from a capture file. What is the MD5 hash value of extracted image?


## Packet Filtering

Helps analysts narrow down traffic and focus on the events of interest. Filters are specific queries designed for protocols available in Wireshark. The two ways to filter traffic are through **queries** and using the **right-click menu**

<u><b>Apply as Filter</b></u>
<span style="color:rgb(0, 176, 80)">Analyze --> Apply as Filter</span>

You can click on the field you want to filter and filter the specific value

<u><b>Conversation filter </b></u>
<span style="color:rgb(0, 176, 80)">Analyze --> Conversation Filter</span>

Allows you to view only the related packets and hide the rest of the packets 

<u><b>Colorized conversation </b></u>
<span style="color:rgb(0, 176, 80)">View --> Colourise Conversation</span>

Similar to conversation filter except it highlights the linked packets without applying a display filter and decreasing the number of viewed packets

 <u><b>Prepare as Filter</b></u>
Similar to Apply as Filter, however it adds the query to the pane and waits for the execution command (enter) or another chosen filtering option by using the **.. and/or.."** from the **right-click menu**

 <u><b>Apply as Column  </b></u>
<span style="color:rgb(0, 176, 80)">Analyse  -->  Apply as Column</span>

adds columns to the packet list pane.

 <u><b>Follow Stream </b></u>

<span style="color:rgb(0, 176, 80)">Analyse --> Follow TCP/UDP/HTTP Stream</span>

It is possible to reconstruct the streams and view the raw traffic as it is presented at the application level. Following the protocol  streams help analysts recreate the application-level data and understand the event of interest. It is also possible to view the unencrypted protocol data like usernames, passwords and other transferred data.