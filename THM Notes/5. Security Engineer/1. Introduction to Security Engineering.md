# Security Engineer Intro
## What is a security engineer
- Main person responsible for organizations assets
- Architects and engineers trustworthy, reliable and secure systems
- Engineer takes large problems, breaks them down into chunks, and solves them

## Core Responsibilities
One of the primary steps in ensuring an organizations security is to maintain the inventory. The must regularly maintain info of assets such as <span style="color:rgb(255, 0, 0)">name, type, IP address, physical location, place in network, applications running on asset, access permissions, and the asset owner details</span> 

A security engineer helps the organization create security policies based on Security Principles. They ensure the organization is secure by design.

## Continuous  Improvement

**Risk** - engineers are often tasked with identifying security risks, determine likelihood of impact, and finding solutions to minimize those risks. Risks are sometimes accepted or mitigated as a business decision

**Change Management** - The security engineer keeps tracks of changes in the organization's digital assets that can affect the security posture and take measures to improve the security posture within the  organizations evolution

**Vulnerability Management** - monitors vulnerabilities across the organization and planning to patch or minimize their risk. Vulnerabilities are generally patched by severity

**Compliance and audit** - Abide by various compliance standards such as PCI-DSS, HIPAA, SOC2, ISO27001, NIST-800-53

## Additional Roles and Responsibilities

Manage Security tooling - may be required to  configure or fine-tune security tools such as SIEMs, firewalls, WAFs, EDRs, and more.

Tabletop exercises - Gauges the operational readiness of an organization from a security standpoint

Disaster Recovery and Crisis Management -  top priority of the executive management is to maintain business continuity

# Security Principles

## CIA

**Confidentiality** - only the intended people can access the data
**Integrity** - Ensure data cannot be altered, detects if alteration occurs
**Availability** -  system is available when needed

<span style="color:rgb(255, 0, 0)">Parkerian Hexad</span>

**Availability** - system is available when needed
**Utility** - usefulness of information
**Integrity** - Ensure data cannot be altered, detects if alteration occurs
**Authenticity**/**Nonrepudiation** - ensuring data is not fraudulent or counterfeit
**Confidentiality** - only the intended people can access the data
**Possession** - protects data from being taken, copied, or controlled

## DAD

<font size=4>Opposite of CIA</font>

**Disclosure** 
**Alteration** 
**Destruction**/**Denial**

## Fundamental Concepts of Security Models

<u><b>Bell-LaPadula Model</b></u> 

Aims to achieve <u>confidentiality</u> by specifying three rules:

**Simple Security Property** -subject at a lower level cannot read an object at a higher level
**Star Security Property** - Subjects at a higher security level cannot write to an object at a lower security level
**Discretionary-Security Property** -  uses a matrix to allow read an write operations. <span style="color:rgb(255, 0, 0)">EX</span>:

| Subject   | Object A   | Object A  |
| --------- | ---------- | --------- |
| Subject 1 | Write      | No Access |
| Subject 2 | Read/Write | Read      |
<span style="color:rgb(255, 0, 0)">Write up, read down</span>

<u><b>Biba Model</b></u>

Aims to achieve <u>integrity</u> through three rules:

**Simple Security Property** - a higher integrity subject should not read from a lower integrity object
**Star Security Property** - a lower integrity subject should not write up to a higher integrity object

<span style="color:rgb(255, 0, 0)">Write down, read up</span>

 <u><b>Clark-Wilson Model</b></u>

Constrained Data Item (CDI) - the data type whos integrity we want to preserve
Unconstrained Data Item (UDI) - this refers to the data type beyond CDI, such as user and system input
Transformation Procedures (TPs) - programmed operations, such as read and write
Integrity Verification Procedures (IVPs) - ensure validity of CDIs

## ISO/IEC 19249

## Zero Trust vs Trust but Verify

**Trust but verify** - always verify even when we trust an entity and its behavior
**Zero Trust** - treats trust as a vulnerability, caters to insider related threats; never trust, always verify. Microsegmentation is one of the implementations of zero trust.

## Threat vs Risk

**Vulnerability** - avenue a breach takes
**Threat** - potential danger associated with a weakness or vulnerability
**Risk** - likelihood that a threat will exploit a vulnerability

# Introduction to Cryptography

**Cryptographic** algorithm or cipher - defines the encryption and decryption process
**Key** - converts plain text to ciphertext and vice versa

### Symmetric Encryption

Symmetric encryption uses same key for encryption and decryption. Requires the users to find a secure channel to exchange keys

| DES 56          | BLOWFISH<br>             |
| --------------- | ------------------------ |
| 3DES            | TWOFISH                  |
| AES             | CAMELLIA128,192, and 256 |
| CAST5 (CAST128) |                          |
All the algorithms mentioned so far are **block cipher** symmetric encryption algorithms. A block cipher algorithm converts the input (plaintext) into blocks and encrypts each block. A block is usually 128 bits.

**stream ciphers** encrypt the plaintext byte by byte.

<u><b>GNU Privacy Guard </u></b>

**encrypt a file**: <span style="font-weight:bold; color:rgb(255, 0, 0)">gpg --symmetric --cipher-algo CIPHER message.txt</span>, where CIPHER is the name of the encryption algorithm. check supported ciphers using **<span style="font-weight:bold; color:rgb(255, 0, 0)">gpg --version</span>** 

**decrypt a file**: **<span style="font-weight:bold; color:rgb(255, 0, 0)">gpg --output original_message.txt --decrypt message.gpg</span>** 

<u><b>OpenSSL Project </u></b>

encrypt a file: **<span style="font-weight:bold; color:rgb(255, 0, 0)"> openssl aes-256-cbc -e -in message.txt -out encrypted_message</span>**

**decrypt a file**: **<span style="font-weight:bold; color:rgb(255, 0, 0)">openssl aes-256-cbc -d -in encrypted_message -out original_message.txt</span>**

### Asymmetric Encryption

Requires the users to find a reliable channel to exchange keys.

If a message is encrypted with one key, it can be decrypted with the other. In other words:

- If Alice encrypts a message using Bob’s public key, it can be decrypted only using Bob’s private key.
- Reversely, if Bob encrypts a message using his private key, it can only be decrypted using Bob’s public key.

Asymmetric encryption solves integrity, authenticity, and nonrepudiation

### Diffie-Hellman Key Exchange
![[Diffie Hellman.png| 500]]

### Hashing

A hash function is an algorithm that takes data of an arbitrary size and inputs and returns a fixed value called a a digest or a checksum. Use hashes to 

- Store passwords
- Verify integrity

### PKI and SSL/TLS

For a certificate to get signed by a certificate authority, we need to:

1. Generate Certificate Signing Request (CSR): You create a certificate and send your public key to be signed by a third party.
2. Send your CSR to a Certificate Authority (CA): The purpose is for the CA to sign your certificate. The alternative and usually insecure solution would be to self-sign your certificate.

# Identity and Access Management

## IAAA Model

1. Identification - user claims a specific identity. Examples: email address, username, or ID number
2. Authentication - ensuring a user is who they say they are; confirming their identity. Ex: password
3. Authorization - determines what a user is allowed to access; Typically enforced through permissions (Access Control) and Least Privilege
4. Accountability - tracks users to ensure they are responsible for their actions. Enforced through auditing and logging user activity 
	1. Logs should be tamper-proof. The reason is that you don’t want the attacker to delete or alter the logs and hide their actions on the network. This is why it is a good practice to set up a separate logging server with one task: receive and store the logs securely. Hence we have log forwarding. **<span style="font-weight:bold; color:rgb(255, 0, 0)">Log forwarding</span>** is the process of sending log data from one system to another.


## Identity Management

Identity Management (IdM) includes all necessary policies and technologies for identification, authentication, and authorization. The main goal is to ensure that only authorized individuals have access to specific resources and information. IdM systems generally include features such as user provisioning, authentication, and authorization. IdM systems are critical in orgs where there are multiple systems and applications that require access control. They act as a single point of reference

Identity and Access Management (IAM) encompasses all the process and technologies to manage and secure digital identities and rights. IAM system functions include provisioning, access control, <u>identity governance</u>, and <u>compliance management</u>. Ensures only authorized users have access to specific resources and data and that their access is monitored and controlled. IAM systems use various technologies to manage access, including role-based access control, multi-factor authentication, and single sign-on. IAM systems help organizations comply with regulatory requirements such as HIPAA, GDPR, and PCI DSS


