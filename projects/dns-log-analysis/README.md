# DNS Log Analysis with Splunk

## Project Overview

This project focuses on DNS traffic analysis using Splunk Enterprise and a dataset containing over 422,000 DNS log events.

The goal of the project was to simulate a basic SOC investigation workflow by:

* Ingesting DNS logs into Splunk
* Performing DNS traffic analysis
* Identifying suspicious or unusual DNS activity
* Building dashboards for traffic visualization
* Conducting basic threat hunting and enrichment analysis
* Documenting findings and investigation methodology

The DNS log dataset used in this project was obtained from a public GitHub repository and imported into a custom Splunk lab environment for analysis.

---

# Technologies Used

* Splunk Enterprise
* SPL (Search Processing Language)
* DNS Log Analysis
* Threat Intelligence Enrichment
* VirusTotal
* AbuseIPDB
* VMware Workstation
* Windows 11 VM
* Ubuntu Server (Splunk Server)
---

# Dataset Information

| Item         | Value          |
| ------------ | -------------- |
| Data Type    | DNS Logs       |
| Total Events | 422,130        |
| Source Type  | dns_logs       |
| Splunk Index | soc-splunk-lab |

---

# Investigation Objectives

The project focused on:

* Understanding baseline DNS activity
* Identifying the most active hosts and domains
* Detecting rare or suspicious DNS queries
* Investigating uncommon TLD activity
* Performing time-based DNS traffic analysis
* Reviewing suspicious domains using external threat intelligence platforms

---

# Key Analysis Performed

## Baseline DNS Analysis

* Total DNS event count
* Top queried domains
* Top source IP addresses
* Unique queried domains by source IP

## DNS Hunting & Investigation

* Long DNS query detection
* Rare DNS query analysis
* Suspicious TLD investigation
* Threat intelligence enrichment using VirusTotal and AbuseIPDB

## Time-Based Analysis

* DNS traffic activity over time
* DNS traffic spike visualization
* Timestamp extraction and normalization for Splunk `_time` usage

---

# Dashboards

The following dashboards were created during the investigation:

* Top Queried Domains
* Top Source IP Addresses
* DNS Activity Over Time

Dashboard screenshots are available in:

```text
projects/dns-log-analysis/Dashboards/
```

---

# Findings Summary

## Suspicious Domain Activity

The investigation identified DNS requests to suspicious or uncommon domains, including:

```text
www.ironwarez.info
```

The domain was reviewed using VirusTotal and AbuseIPDB and was flagged as malicious/suspicious during enrichment analysis.

Repeated DNS activity associated with this domain was observed from internal hosts within the dataset.

---

## P2P / Torrent-Related Activity

Rare DNS query analysis identified traffic related to torrent/P2P-associated infrastructure, including:

```text
update.utorrent.com
search.vuze.com
```

The analysis identified internal hosts performing DNS requests to these services.

While this does not confirm malicious activity, it may indicate the use of unauthorized or potentially unwanted software.

---

# Project Structure

```text
projects/dns-log-analysis/
│
├── Dashboards/
├── screenshots/
├── README.md
├── findings.md
├── investigation-notes.md
└── spl-queries.md
```

---

# Screenshots

Project screenshots include:

* Splunk dashboards
* DNS query investigations
* Suspicious domain analysis
* DNS traffic visualizations
* Threat hunting results

All screenshots are stored in:

```text
projects/dns-log-analysis/screenshots/
projects/dns-log-analysis/Dashboards/
פר
```

---

# Learning Outcomes

This project helped develop practical experience with:

* Splunk search and analysis
* DNS traffic investigation
* Threat hunting methodology
* Basic SIEM workflow
* Dashboard creation
* Data parsing and field extraction
* Time-based event analysis
* Threat intelligence enrichment

---

# Notes

This project was created as part of a hands-on SOC and SIEM learning process focused on practical investigation workflows and DNS traffic analysis.

The project is intended for educational and portfolio purposes.


