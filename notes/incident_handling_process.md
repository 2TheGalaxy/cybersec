# Incident handling process

## Cyber Kill Chain
##
    Recon -> Weaponize -> Deliver -> Exploit -> Install -> C&C -> Action
##

### Stages of the Cyber Kill Chain

#### Recon
Attacker choosing target and gathering information about it

- Active Recon
  - Identify the target & scope of target network
  - Locate Open Ports
  - Identify services running on open ports
  - Map entire network

- Passive Recon
  - Information gathering from web sourcer (Job Ads, Company partenrs, etc.)
  - Socail Media (LinkedIn, Instagram, Facebook, etc.)
  - Avoid detection all the time

#### Weaponize
Exploit / payload / malware is crafted/developed to be used on the target.

#### Delivery
Exploit / payload / maware is delivered to the victim(s) via some delivery
mechanism, for example via phising emails.

#### Exploitation
Exploit / malware is delivered and the payload is triggered.
Execution of code on the target system to gain access or control

#### Installation
Initial stagger is executed and is running on the compromised machine.

Some techniques used:
- Droppers - small piece of code designed to install malware.
- Backdoors - malware designed to provide the attacker with ongoin access.
- Rootkits - malvare designed its presence.

#### C&C (Command and Control)
Attacker establishes a remote access capability.

#### Action
The objective of the attack like exfiltrating confidential data.


### OUR OBJECTIVE IS TO STOP ATTACKER FROM PROGRESSING UP THE KILL CHAIN

## MITRE ATT&CK Framework
https://attack.mitre.org/

**TTPs** (Tactics, Techniques, Procedures)

- Tactics (eg. Initial Access, Persistence)
- Techniques (eg. T1105 - Ingress Tool Transfer)
- Subtechnique (eg. T1003.001 - Os Credentials: LSASS Memory)

### Pyramid of Pain
Ilustrates how much effort it takes for adversary to change their tactics when
defenders detect and block different types of indicators.

    TTPs (ATT&CK)               - Tough
    Tools                       - Challenging
    Network / Host Artifacts    - Annoying
    Domain Names                - Simple
    IP Addresses                - Easy
    Hash Values                 - Trivial

### MITRE ATT&CK integration in **TheHive**
**TheHive** is a case management platform designed for cybersecurity teams
to efficiently handle incidents by processing alerts.

# Incident Handling Process Overview

    Preparation  
    ^         |
    |         v
    |  .--> Detection and Analysis --.
    |  :         |                   : 
    |  :         v                   v
    |  '--- Containment, Eradication and Recovery
    |          |
    |          v
    Post-Incident Activity

Incident handlers spend most of their time in the first two stages,
**preparation** and **detection and analysis**


Incident handling has two main activities:
- Investigation
  - Discover the initial '**patient zero**' and create incident timeline
  - Determine which **tools** and malware the adversary used
  - **Document** the compromised systems and what the adversary has done
- Recovering
  - Creating and implementing a **recovery plan** 


# Preparation Stage

#### Preparation prerequisites
- Incident handling capability within the organization
- Protect against & prevent IT security incidents
- Clear Policies
- Documentation
- Tools (Software & Hardware)

"**JUMP BAG**" - always ready with necessary tools

### DMARC
(Domain-based Message Authentication, Reporting & Conformance) is an email 
protection mechanism

---glossary---
- **SPF** (Sender Policy Framework) is an email authentication protocol
  designed to prevent email spoofing
- **DKIM** (DomainKeys Identified Mail) is an email authentication protocol
  that uses public-key cryptography to verify
------

### Endpoint Hardening (& EDR)
Highly important actions:
- Disable **LLMNR / NetBIOS**
- Implement **LAPS** and remove admin privilages from regular users
- Enable **Attack Surface Reduction (ASR)** for MC Defender
- Implement whitelisting when possible
- Utilize host-based firewalls
- Deploy an **EDR (Endpoint Detection and Response)**

### Network Protection
Network segmentation is a powerful technique for preventing a breach from
spreading across the entire organization.
Business-critical systems must be isolated, and connections should be allowed
only as required by the business.
Internal resources should not face the Internet directly (unless placed in DMZ).

Consider **IDS/IPS (Intrusion Detection System / Intrusion Prevention System)**.
Their power shines when **SSL/TLS** interception is performed so that they can
identify malicious traffic based on the wire and not based on the reputation of
the IP addresses.

Ensure that only organization-approved devices can access the network.
Solutions such as 802.1x can be utilized to reduce the risk of
**bring your own device (BYOD)** or malicous devices connecting to the
corporate network.
If we are a clud-only, for example Azure/Azure AD (now called Microsoft Entra ID),
then we can achieve similar protection with Conditional Acess policies that
will allow acess to resources only if we are connecting from company-managed device.

### Privilege Identity Management / MFA / Passwords
Stealing credentials is the most common escalation path in AD enviroments.
Common mistake is that admin users either have a weak (but often comples)
passowrd or a shared password with their regular user account.
Weak but complex password is "Password1!". It has upper and lower case, numbers
and special char, but its predictable.
It is recommended to use passphrases like "i Lik3 my coffE warm!".

### Vulnerability Scanning
Perform continuous vulnerability scans of our environment and remediate at 
least the "High" and "Critical" vulnerabilities that are discovered.

### User Awarness Training

### Active Directory Security Assessment

### Purple Team Exercises
Blue and Read team working together to assess the security.


