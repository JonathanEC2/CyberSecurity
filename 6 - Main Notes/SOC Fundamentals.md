---
sr-due: 2025-05-27
sr-interval: 41
sr-ease: 210
---
[[../2 - Tags/Defensive]]

#review 
#defensive_security

# SOC Fundamentals

A Security Operations enter is a dedicated facility operated by a specialized security team. This team works 24 hours a day, seven days a week

## Purpose and Components

The main focus of the SOC is to keep **detection** and **response** in tact. Continuous monitoring is required to detect and respond to any security incident

#### Detection

- **Detect vulnerabilities**: a vulnerability is a weakness in a system that an attacker can exploit to carry out things beyond their permission level. Vulnerabilities are not necessarily the SOCs responsibility; however, unfixed vulnerabilities affect the security level of the entire company
- **Detect unauthorized activity**: example would be a user logging in from a suspicious location
- **Detect policy violations**: A security policy is a set of rules and procedures created to help protect a company against security threats and ensure compliance
- **Detect intrusions**: intrusions refer to unauthorized access to systems and networks

#### Response

**Support with the incident response**: Once an incident is detected, certain steps are taken to respond to it. This response includes minimizing its impact and performing the root cause analysis of the incident

The three pillars of a SOC are People, Process, and Technology

## People

Roles and responsibilities of SOC team


- **SOC Analyst (Level 1):** Anything detected by the security solution would pass through these analysts first. These are the first responders to any detection. SOC Level 1 Analysts perform basic alert triage to determine if a specific detection is harmful. They also report these detections through proper channels.
- **SOC Analyst (Level 2):**  Level 2 Analysts  dive deeper into the investigations and correlate the data from multiple data sources to perform a proper analysis.
- **SOC Analyst (Level 3):** Level 3 Analysts are experienced professionals who proactively look for any threat indicators and support in the incident response activities. The critical severity detection reported by Level 1 and Level 2 Analysts are often security incidents that need detailed responses, including containment, eradication, and recovery. This is where Level 3 analysts’ experience comes in handy.
- **Security Engineer**: All analysts work on security solutions. These solutions need deployment and configuration. Security Engineers deploy and configure these security solutions to ensure their smooth operation.
- **Detection Engineer**: Security rules are the logic built behind security solutions to detect harmful activities. Level 2 and 3 Analysts often create these rules, while the SOC team can sometimes also utilize the detection engineer role independently for this responsibility.
- **SOC Manager**: The SOC Manager manages the processes the SOC team follows and provides support. The SOC Manager also remains in contact with the organization’s CISO (Chief Information Security Officer) to provide him with updates on the SOC team’s current security posture and efforts.

## Process

Each role has its own process,  just as we saw the role of Level 1 SOC Analysts as the first responders to carry out alert triage and determine if it is harmful. 

#### Alert Triage

The alert triage is the basis of the SOC team. The first response to any alert is to perform the triage. This helps determine the severity of the alert and helps us prioritize it. The triage is all about answering the 5 W's:
- Who 
- What 
- Where 
- When
- Why

The detected harmful alerts need to be escalated to higher level analysts for a timely response and resolution. These alerts are escalated as tickets and assigned to relevant people. 

## Technology

This refers to the security solutions. These solutions efficiently minimize the SOC teams manual effort to detect and respond to threats. Security solutions centralize all the information of the device or applications present in the network and automate the detection and response capabilities

**SIEM**: Security Information and Event Management is a popular tool used by every SOC environment. It collects logs form various network devices, referred to as source logs. Detection rules are configured in the SIEM solution which contains logic to identify suspicious activity.  The SIEM solution provides us with the detections after correlating them with multiple log sources and alerts us in case of a match with any of the rules

**EDR**;; Endpoint Detection and Response provides the SOC with real time and historical visibility of the devices' activities. EDR has extensive detection capabilities for endpoints, allowing you to investigate them in detail and respond with a few clicks.
<!--SR:!2025-06-12,30,170-->

**Firewall**: functions purely for network security and acts as a barrier between your internal and external networks.  It monitors incoming and outgoing network traffic and filters any unauthorized traffic. The firewall also has some detection rules deployed, which help us identify and block suspicious traffic before it reaches the internal network.