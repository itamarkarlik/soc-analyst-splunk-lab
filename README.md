# DNS Log Analysis with Splunk

## Project Overview

This project focuses on DNS traffic analysis using Splunk Enterprise and a dataset containing over 422,000 DNS log events.

The investigation included:

- DNS traffic analysis
- Threat hunting
- Suspicious domain investigation
- Time-based DNS analysis
- Dashboard creation
- Threat intelligence enrichment using VirusTotal and AbuseIPDB

The DNS dataset was imported into a custom Splunk lab environment for analysis and investigation.

---

## Technologies Used

- Splunk Enterprise
- SPL (Search Processing Language)
- VMware Workstation
- Ubuntu Server (Splunk Server)
- Windows 11 VM
- VirusTotal
- AbuseIPDB

---

## Dataset Information

| Item | Value |
|---|---|
| Data Type | DNS Logs |
| Total Events | 422,130 |
| Source Type | dns_logs |
| Splunk Index | soc-splunk-lab |

## Dataset Source

The DNS log dataset used in this project was obtained from the following public repository:

https://github.com/0xrajneesh/Splunk-Projects-For-Beginners

The dataset was imported into a custom Splunk lab environment and analyzed as part of this investigation project.


---

## Key Analysis Performed

- Total DNS event analysis
- Top queried domains
- Top source IP addresses
- Rare DNS query analysis
- Suspicious TLD investigation
- Long DNS query detection
- DNS traffic analysis over time
- Threat intelligence enrichment
- Source IP correlation

---

## Dashboards

The following dashboards were created during the investigation:

- Top Queried Domains
- Top Source IP Addresses
- DNS Activity Over Time

---

## Findings Summary

### Suspicious Domain Activity

The investigation identified repeated DNS requests associated with:

```text
www.ironwarez.info
```

The domain was flagged as suspicious/malicious during external threat intelligence enrichment analysis.

---

### P2P / Torrent-Related Activity

Rare DNS query analysis identified DNS requests related to torrent/P2P-associated services, including:

```text
update.utorrent.com
search.vuze.com
```

The activity originated from multiple internal hosts within the dataset.

---

## Project Structure

```text
dns-log-analysis/
│
├── Dashboards/
├── screenshots/
├── README.md
├── findings.md
├── investigation-notes.md
└── spl-queries.md
```
