# Introduction to The Elastic Stack
### What is the Elastic Stack?
Open-source collection of applications for search, visualization,
real-time analysis and exploration of log file sources.

                  | [Kibana]           |- Visualize
    Elastic Stack | [Elasticsearch]    |- Store Search & Analyze
                  | [Beats] [Logstash] |- Ingest

Can be enchanced by addition of **Kafka**, **RabbitMQ** and **Redis**
for buffering and resiliency and **nginx** for security.

#### Elasticsearch
JSON-based with RESTful APIs, search engine to perform searches and perform
analytics on log files processed by Logstash

#### Logstash
Collecting, transforming, transporting log file records.
Consolidate and normalize data from sources.
- Process input
- Transform and enrich log records
- Send it to Elasticsearch

#### Kibana
Visualization tool for Elasticsearch documents

#### Beats
Additional data shipper designed to be installed on remote machines to
forward logs and metrics.

      Beats -> Logstash -> Elasticsearch -> Kibana
              or
      Beats -> Elasticsearch -> Kibana

## The Elastic as a SIEM Solution
### How to identify available data
- Kibana Query Language (KQL)
  - **field:value** pairs (eg. **event.code:4625**)

- Elastic Documentation

### The Elastic Common Schema (ECS)
Shared and extensible vocabulary for event logs across the Elastic Stack
