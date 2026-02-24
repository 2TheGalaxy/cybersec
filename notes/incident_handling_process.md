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
    ^        |
    |        v
    |   .--> Detection and Analysis --.
    |   :    |                        : 
    |   :    v                        v
    |   '--- Containment, Eradication and Recovery
    |        |
    |        v
    Post-Incident Activity
