# Governance and Regulation
## Why is it Important

Governance: Managing and directing an organization or system to achieve its objectives and unsure compliance with laws, regulations, and standards
Regulation: rule enforced by a governing body to ensure compliance; Ex:  General Data Protection Regulation (GDPR), Payment Card Industry Data Security Standard (PCI DSS)
Compliance: adhering to laws, regulations, and standards

## Information Security Frameworks

- **Policies**: A formal statement that outlines an organization's goals, principles, and guidelines for achieving specific objectives.
- **Standards**: A document establishing specific requirements or specifications for a particular process, product, or service.
- **Guidelines**: A document that provides recommendations and best practices (non-mandatory) for achieving specific goals or objectives.
- **Procedures**: Set of specific steps for undertaking a particular task or process.
- **Baselines**: A set of minimum security standards or requirements that an organization or system must meet.

## Governance Risk and Compliance (GRC)

- **Governance Component:** Involves guiding an organization by setting its direction through information security strategy,  which includes policies, standards, baselines, frameworks, etc.
- **Risk Management Component**: Involves identifying, assessing, and prioritizing risks to the organization and implementing controls and mitigation strategies to manage those risks effectively. This includes monitoring and reporting on risks and continuously evaluating and refining the risk management program to ensure its ongoing effectiveness.
- **Compliance Component**: Ensuring that the organisation meets its legal, regulatory, and industry obligations and that its activities align with its policies and procedures.
## NIST Special Publications

NIST 800-53 is a publication titled "**Security and Privacy Controls for Information Systems and Organizations**",  developed by the National Institute of Standards and Technology (NIST), US, that provides a catalogue of security controls to protect the CIA triad of information systems. The publication serves as a framework for organizations to assess and enhance the security and privacy of their information systems and comply with various laws, regulations, and policies. 

## Information Security Management and Compliance

ISO 27001 is an internationally recognized standard for requirements to plan, develop, run, and update an organization's Information Security Management System (ISMS).

# Threat Modelling

## Threat Modelling Overview

Threat modelling is a systematic approach to identifying, prioritizing, and addressing potential security threats across the organization by simulating possible attack scenarios and assessing the existing vulnerabilities of the organizations interconnected systems and applications

Threat: anything that has the potential to compromise CIA
Vulnerability: Weakness in a system
Risk: Possibility of a threat taking advantage of a vulnerability (how successful an attack might be and how much damage it could cause)

<u>High-Level Process of Threat Modelling</u>
1. **Defining the scope**
2. **Asset Identification**
3. **Identify Threats**
4. **Analyze Vulnerabilities and Prioritize Risks** 
5. **Develop and Implement Countermeasures**
6. **Monitor and Evaluate**
### Attack Tree

Graphical representation used in threat modelling to describe and analyze potential threats against a system or infrastructure; breaks down attack scenarios into smaller components

![[Pasted image 20241008144611.png]]

## Modelling with MITRE ATT&CK

MITRE ATT&CK (Adversarial Tactics, Techniques, and Common Knowledge) is a knowledge base of cyber adversary behaviors and tactics. Help understand the different stages of cyber attacks and develop effective defenses

## Mapping with ATT&CK Navigator

The MITRE ATT&CK Navigator is an open-source, web-based tool that helps visualize and navigate the complex landscape of the MITRE ATT&CK Framework.

## DREAD Framework

Framework developed by Microsoft to <u>evaluate and prioritize threats and vulnerabilities</u>

| DREAD           | Definition                                                                                    |
| --------------- | --------------------------------------------------------------------------------------------- |
| Damage          | Potential harm from exploiting a vlunerability                                                |
| Reproducibility | Ease in which an attacker can recreate the exploitation of a vulnerability                    |
| Exploitability  | Difficulty involved in exploiting the vulnerability such as skill, tool availabilty, and time |
| Affected Users  | Users impacted                                                                                |
| Discoverability | Ease in which attacker can identify the vulnerability                                         |

## STRIDE Framework

Framework developed by Microsoft to <u> helps identify and categorize potential security threats in software development and system design</u>\

| STRIDE                 | Definition                                                   | Policy Violated |
| ---------------------- | ------------------------------------------------------------ | --------------- |
| Spoofing               | Unauthorized access                                          | Authentication  |
| Tampering              | Unauthorized modification                                    | Integrity       |
| Repudiation            | Denting having acted due to insufficient auditing or logging | Non-repudiation |
| Info Disclosure        | Unauthorized access to sensitive information                 | Confidentiality |
| Denial of Service      | Inability to access system                                   | Availability    |
| Elevation of Privilege | Unauthorized access to access privileges                     | Authorization   |

## Pasta Framework

![[Pasted image 20241009193437.png]]


# Risk Management

Process of identifying, assessing, and responding to risks associated with a specific activity

## Basic Terminology

**Threat**: intentional or accidental event that can compromise the security of an info system. Can be human, technical, or natural
**Vulnerability**: Weakness in a system that can be exploited (Hardware, software, data, documentation)
**Asset**: valued resource or component that an org relies on to achieve its goals
**Risk**: possibility of a threat source exploiting a vulnerability 
**Risk management**:  process of identifying, assessing, and responding to risks associated with a particular situation or activity.

### Risk Assessment Methodologies

NIST SP 800-30: Identifies and evaluates risk, determining the likelihood and impact of each risk, and developing a risk response plan

Based on NIST SP 800-30, the risk management process entails four steps:

- Frame risk
- Assess Risk
- Respond to risk
- Monitor risk


## Frame Risk

Sets the groundwork for managing risk and provides limits to risk-based decisions. To create a a risk frame, identify:

**Risk assumptions:** What can we assume about the threats and vuln? What is the likelihood of occurrence? What would be the impact and consequences?
**Risk Constraints**: What are the constraints of assessing, responding, and monitoring risks?
**Risk Tolerance**: What is an acceptable level of risk and risk uncertainty?
**Priorities and Trade-offs**: What are the high-priority business functions? What are the trade-offs among the different types of faced risks?

## Assess Risk

The goal of risk assessment is to determine:

- Threats
- Vulnerabilities
- Impact
- Likelihood

## Risk Analysis

#### Qualitative Risk
Qualitative: High, medium, low
![[Pasted image 20241022144904.png]]

#### Quantitative Risk
Quantitative: Monetary value

<u>Single Loss Expectancy </u>
SLE = AssetValue x EF

Where:

- **Single Loss Expectancy (SLE)** is the loss incurred due to the realization of a threat represented as a monetary value.
- **Asset Value** is the monetary valuation of an asset
- **Exposure Factor (EF)** is the percentage of loss a realized threat can cause to an asset.

<u>Annual Loss Expectancy </u>

ALE = SLE × ARO

Where:

Annualized Loss Expectancy (ALE) is the loss the company expects to lose per year due to the threat.
Annualized Rate of Occurrence (ARO) is the expected number of times this threat is realized yearly, i.e., frequency per year.

## Respond to Risk

- Avoid Risk
- Transfer Risk
- Mitigate Risk
- Accept Risk

<span style="color:rgb(255, 0, 0)">ValueofSafeguard</span> = <span style="color:rgb(255, 0, 0)">ALEbeforeSafeguard − ALEafterSafeguard − AnnualCostSafeguard</span> 

# Vulnerability Management 

## Vulnerability Management vs Vulnerability Scanning

**Vulnerability management** aims to lower an organization's overall risk exposure by promptly identifying and mitigation as many vulnerabilities as possible. Encompasses vulnerability scanning


## Vulnerability Classification

Common Vulnerabilities and Exposures (CVE): standardizes the identification of security vulnerabilities

## Vulnerability Management Lifecycle - Discover & Prioritize

List all the assets in the environment including application, services, OS, and configurations to identify vulnerabilities. Typically this combines both a network and a systems scan. Odfrganization-wide scanning should be planned and conducted regularly.

Group and assign risk-based priority to assets based on how critical they are to business. This significantly assists the org in determining what requires special attention and will aid in the decision  making process

**<span style="font-weight:bold; color:rgb(255, 0, 0)">Asset vulnerabilities leading to data breaches and DB access are rated as Top risk priority</span>**
## Vulnerability Management Lifecycle - Assess & Report

Create a risk baseline by evaluating assets to determine how severe each is. The process lets organization's decide which risks to eliminate based on factors such as their classification, criticality level, and vulnerability level.

Documenting and reporting are crucial for engineers because it makes it easier for engineers to monitor vulnerability dynamics throughout the network
## Vulnerability Management Lifecycle - Remediate &Verify

Remedial action, such as thoroughly addressing or patching vulnerabilities, is the best course of action.  If complete remediation is not feasible, businesses might mitigate, which entails lowering the risk of exploitation or minimizing the potential harm.

## Vulnerability Management Framework

<u>NIST Cybersecurity Framework</u>

![[NIST Framework.png]]

#### Identify
#### Protect
#### Detect
#### Respond
#### Discover