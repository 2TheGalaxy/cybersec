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

#### timerange
    index="main" earliest=-7d EventCode!=1

#### **transactions**
    index="main" sourcetype="WinEventLog:Sysmon" (EventCode=1 OR EventCode=3)
    | transaction Image startswith=eval(EventCode=1) endswith=eval(EventCode=3) maxspan=1m
    | table Image
    | dedup Image  

- index="main" sourcetype="WinEventLog:Sysmon" (EventCode=1 OR EventCode=3):
  This is the search criteria. It's pulling from the main index where the
  sourcetype is WinEventLog:Sysmon and the EventCode is either 1 or 3.
  In Sysmon logs, EventCode 1 refers to a process creation event, and
  EventCode 3 refers to a network connection event.
- | transaction Image startswith=eval(EventCode=1) endswith=eval(EventCode=3) maxspan=1m:
  The transaction command is used here to group events based on the Image
  field, which represents the executable or script involved in the event.
  This grouping is subject to the conditions: the transaction starts with an
  event where EventCode is 1 and ends with an event where EventCode is 3.
  The maxspan=1m clause limits the transaction to events occurring within a
  1-minute window. The transaction command can link together related events
  to provide a better understanding of the sequences of activities happening
  within a system.

this query aims to identify sequences of activities
(process creation followed by a network connection)

#### subsearch
    ... [search ...]

### Identify available data

#### event count / summarize (note no "..." at the beginning)
    | eventcount summarize=false index=*
    | table index, count

#### metadata
    | metadata type=sourcetypes
####
    | metadata type=sources

#### raw data from a specific log or log type
    sourcetype="WinEventLog:Security"
    | table _raw
