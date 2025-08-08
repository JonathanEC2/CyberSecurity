#security_solutions
[[../2 - Tags/Security Solutions|Security Solutions]]

# IDS Fundamentals

## What is an IDS

Detects the activities of the  connections that pass through the firewall. If an attacker successfully passes a firewall via a legitimate-looking connection and then performs any malicious activity, there should be something to detect it timely. 

If a firewall is a gate keeper, the IDS would act as the surveillance cameras. If the gatekeeper missed the threat at the gate, the IDS would detect them. It sits in a corner, monitors the network traffic based on its signature and anomaly-based detections, and detects any abnormal traffic going out or inside the network. Upon every detection, an alert is generated for the security administrators. IDS does not act on those detections; it only notifies the security administrators about the malicious activity.

## Types of IDS

### Deployment Modes

**Host Intrusion Detection System (HIDS)**: Installed individually on the hosts and are responsible for only detecting potential security threats associated with a particular host. Challenging to manage in large networks as they are resource-intensive and require management on each host.

**Network Intrusion Detection System (NIDS)**: Crucial in detecting potentially malicious activities within the whole network, regardless of  any specific host. Provides a centralized view of all detections inside the network

### Detection Modes

**Signature-Based IDS**:  Each attack has its unique pattern, which is known as a signature. These signatures are preserved by the IDS in their database so if the attack happens again, it gets detected by its signature and reported to the security administrators for action. Unable to detect zero-day attacks.

**Anomaly-Based IDS:**  learns the normal behavior (baseline) of the network or system and performs detections if there is any deviation from the normal behavior. Anomaly-based IDS can also detect zero-day attacks. This IDS may generate a lot of false positives because the nature of most legitimate programs match malicious ones

**Hybrid IDS:** A hybrid IDS combines the detection methods of signature-based IDS and anomaly-based IDS to leverage the strengths of each approach.

## IDS Example: Snort

Uses signature-based and anomaly-based detections to identify known threats. These are defined in the rule files of the Snort tool. Several built-in rule files come pre-installed in this tool’s package. You can also create custom rules based on your requirements to detect specific traffic. 

|Mode|Description|Use Case|
|---|---|---|
|Packet sniffer mode|This mode reads and displays network packets without performing any analysis on them. The packet sniffer mode of Snort does not directly relate to IDS capabilities, but it can be helpful in network monitoring and troubleshooting. In some cases, system administrators might need to read the traffic flow without performing any detection to diagnose specific issues. In this case, they can utilize the packet sniffer mode of Snort. This mode allows you to display the network traffic on the console or even output it in a file.|The network team observes some network performance issues. To diagnose the issue, they need detailed insights into the network traffic. For this purpose, they can utilize Snort’s packet sniffer mode.|
|Packet logging mode|Snort performs detection on the network traffic in real-time and displays the detections as alerts on the console for the security administrators to take action. However, in some cases, the network traffic needs to be logged for later analysis. The packet logging mode of Snort allows you to log the network traffic as a PCAP (standard packet capture format) file. This includes all the network traffic and any detections from it. Forensic investigators can use these Snort log files to perform the root cause analysis of previous attacks.|The security team needs to initiate a forensic investigation of a network attack. They would need the traffic logs to perform the root cause analysis. The network traffic logged through Snort’s packet logging mode can help them.|
|Network Intrusion Detection System mode|Snort’s NIDS mode is the primary mode that monitors network traffic in real-time and applies its rule files to identify any match to the known attack patterns stored as signatures. If there is a match, it generates an alert. This mode provides the main functionality of an IDS solution.|The security team must proactively monitor their network or systems to detect potential threats. They can leverage Snort’s NIDS mode to achieve this.|

## Snort Usage

You can run Snort normally, where it only captures the traffic intended for your host. However, if you want to use Snort to capture and detect intrusions in your whole network, you must turn on the promiscuous mode of your host’s network interface. 

#### Rule Format

![[../../../attachments/Pasted image 20250311192938.png]]

- **Action**: What action to take when the rule triggers. In this case, we have the action to "alert" when the traffic matches this rule.
- **Protocol**: The protocol that matches this rule. In this case, we use the protocol "ICMP," which is used when we ping a host.
- **Source IP**: Where the traffic is originating. Since we want to detect traffic from any source IP, we set this as "any".
- **Source port**: The port from which the traffic is originating. Since we want to detect traffic from any source port, we set this as "any".
- **Destination IP**: The destination IP to which the matching traffic comes; it generates the alert. In this case, we used "$HOME_NET". This is a variable, and we defined its value as our whole network’s range in the Snort’s configuration file.
- **Destination port**: The port the traffic would reach. As we want to detect traffic coming to any port, we set it as "any".
- **Rule metadata**: Every rule has some metadata. That is defined at the end of the rule in parentheses. The following are its components:
	- **Message (msg)**: This describes the message to be displayed when the subject rule triggers. The message should indicate the type of activity detected. In this case, we used "Ping Detected".
	- **Signature ID (sid)**: Every rule has a unique identifier that differentiates it from the other rules.
	- **Rule revision (rev)**: This sets the revision number of the rule. Every time the rule is modified, its revision number is incremented.


#### Running Snort on PCAP Files

```
sudo snort -q -l /var/log/snort -r Task.pcap -A console -c /etc/snort/snort.conf
```
