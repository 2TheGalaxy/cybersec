# Incident handling process

## Cyber Kill Chain
    Recon -> Weaponize -> Deliver -> Exploit -> Install -> C&C -> Action

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

- **SPF** (Sender Policy Framework) is an email authentication protocol
  designed to prevent email spoofing
- **DKIM** (DomainKeys Identified Mail) is an email authentication protocol
  that uses public-key cryptography to verify

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


# Detection & Analysis Stage
- **Detection**

- **Initial Investigation**
  - establish context
  - date, time
  - who, where
  - etc.

- **Incident Severity & Extent Questions**
  - What is the exploit impact
  - What is required for the exploit
  - What is or can be affected
  - Are there remediation steps
  - How many systems impacted
  - Is the exploit used in the wild
  - Does the exploit have any worm-like capabilities
  Last three possibly indicate sophistication level of the attacker

- **Incident Confidentiality & Communication**
  - who and what to report to

### The Investigation

    Initial investigation data
        |
     __ | _________________________________
    |   v                                  |
    | IOCs (indicators of compromise) <-.  |
    |   |                               :  |
    |   v                               :  |
    | Compromised Systems               :  |
    |   |                               :  |
    |   v                               :  |
    | Collection & Analysis ------------'  |
    |______________________________________|

Do not narrow investigation down but broaden it.

### Creation & usage of IOCs
**IOC (Indicator of Compromise)** - sign that indicent has occured, structured,
artifact of compromise, like:
- IP addresses,
- hash values of files,
- filenames,
- etc.

Widely used standards / special language for IOCs:
- **OpenIOC**
- **YARA**
- **STIX (Structured Threat Information eXpression)**

To leverage IOCs, we will have to deploy an IOC-obtaining/IOC-searching tool
(native or third-party and possibly at scale).
A common approach is to utilize **WMI (Windows Management Instrumentation)** or
PowerShell for IOC-related operations in Windows environments.

----------
**CAUTION**
During investigation prevent highly priviliged user credentials from being
cached eg. WinRM.

**KNOW YOUR TOOLS**
eg. "PsExec":
- when used with explicit credentials, they are cached,
- when used through the session of current user - not cached on remote machine.
----------


### Identification of new leads & impacted systems
- eliminate false positives
- focus on IOCs that give most new leads

### Data collection and analysis from the new leads and impacted systems
- Collect and preserve the sate of impacted systems
- Sometimes we want to perform '**live response**' and sometimes we need to
  shut down affected systems,
- Keep track of the **chain of custody**.

### Use of AI in threat detection
eg. Elastic Security "Attack Discovery"


# Containment, Eradication and Recovery Stage
    Investigation is complete
            |
       ____ v ________________________
      |                               |
      | Containment Strategy          |
      | Evidence Gathering            |
      | Identify the Attacking Host   |
      | Eradication and Recovery      |
      |_______________________________|
                        |
                        v
              Bring Systems Back to Normal

### Containment
- prevent spread
- **short-term containment**:
  - leave unaltered
  - take forensic images / "backup stage"
  - eg. - puting on separate VLAN
- **long-term containment**:
  - persistent actions and changes
  - eg. changing passwords, applying firewall rules

### Eradication
- remove malware
- rebuild some systems or restore backups
- applay patches
- hardening systems

### Recovery
- bring systems back to normal operation
- verify integrity


# Post-Incident Activity Stage

     ______________________________________
    |                                      |
    | Incident Resolved                    |
    |          |                           |
    |          v                           |
    | Post-Incident Review                 |
    |          |                           |
    |          v                           |
    | Lessons Learned Metting              |
    |          |                           |
    |          v                           |
    | Root Cause Analysis                  |
    |          |                           |
    |          v                           |
    | Update Policies and Playbooks        |
    |          |                           |
    |          v                           |
    | Enhance Detection & Monitoring Rules |
    |          |                           |
    |          v                           |
    | Knowledge Sharing & Awarnes          |
    |          |                           |
    |          v                           |
    | Report to Management & Close Case    |
    |______________________________________|

### Reporting
**Crucial part!** A complete report will answer:
- What happened and when
- How did the team perform in dealing with the incident
- Did the business provide necessary information and respong promptly to aid in
  handling the incident
- What actions have beed implemented to contain and eradicate the incident
- What preventive measures for the future
- What tools and resources for the future
