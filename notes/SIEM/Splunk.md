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

### SPL Searching with examples

"search" command is implicit at the beginning
#### operators
    AND, OR, NOT, =, !=, <, >, <=, >=

#### fields 
    index="main" sourcetype="WinEventLog:Sysmon" EventCode=1
    | fields - User

#### table
    ... | table _time, host, Image
Image is the name of executable

#### rename
    ... | rename Image as Process

#### dedup
    ... | dedup Image

#### sort
    ... | sort - _time #recent first
    ... | sort + _time #old first

#### stats
    ... | stats count by _time, Image

#### chart
    ... | chart count by _time, Image

#### eval
    ... | eval Process_Path=lower(Image)

#### regex
    ... | rex max_match=0 "[^%](?<guid>{.*})" | table guid

#### lookup files *.csv
    ... 
    | rex field=Image "(?P<filename>[^\\\]+)$"
    | eval filename=lower(filename)
    | lookup malware_lookup.csv filename OUTPUTNEW is_malware
    | table filename, is_malware
    | dedup filename, is_malware
Settings -> Lookups -> Lookup table files

#### inputlookup (note no "..." at the beginning)
    | inputlookup malware_lookup.csv
This command retrieves all records from the malware_lookup.csv file.
The result is not joined with any search results but can be used to verify the
content of the lookup file or for subsequent operations like filtering or
joining with other datasets.

