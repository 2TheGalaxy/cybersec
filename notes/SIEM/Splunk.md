# Splunk & SPL

**Splunk** - data analysis software solution for indexing, analyzing,
visualizing massive amounts of machine data.

**SPL** - Splunk/Search Processing Language

#### Splunk architecture:
- Forwarers:
  - Uniwersal Forwarder (UF)
  - Heavy Forwarders (HF)
- Indexers
- Search Heads
- Deplyoment Server
- Cluster Master
- License Master

Splunk's key components include:
- Splunk Web Interface
- Splunk/Search Processing Language (SPL)
- Apps and Add-ons
- Knowledge objects


## Splunk as a SIEM Solution

### SPL Searching

"search" command is implicit at the beginning
#### operators
    AND, OR, NOT, =, !=, <, >, <=, >=

#### fields 
    index="main" sourcetype="WinEventLog:Sysmon" EventCode=1
    | fields - User
