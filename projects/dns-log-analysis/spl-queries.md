# SPL Queries

## Total DNS Event Count

```spl
index="soc-splunk-lab" sourcetype="dns_logs"
| stats count
```

### Purpose

Count the total number of DNS events in the dataset.

### Result

422,130 DNS events were identified.

### Screenshot

```text
screenshots/event-count.png
```

---

## Top Queried Domains

```spl
index="soc-splunk-lab" sourcetype="dns_logs"
| stats count by query
| sort - count
| head 10
```

### Purpose

Identify the most frequently queried domains within the DNS dataset.

### Result

The query displayed the top 10 most requested DNS domains based on total query count.  
This helps establish normal DNS activity patterns and identify frequently accessed services or domains.

### Screenshot

```text
Dashboards/top-queried-domains-dashboard.png
```

---

## Top Source IP Addresses

```spl
index="soc-splunk-lab" sourcetype="dns_logs"
| stats count by source_ip
| sort - count
| head 10
```

### Purpose

Identify the most active source IP addresses generating DNS traffic within the dataset.

### Result

The query revealed the top 10 source IP addresses with the highest number of DNS events.  
This helps identify high-activity hosts and establish baseline network behavior.

### Screenshot

```text
Dashboards/top-source-ips.png
```

---

## Unique Queried Domains by Source IP

```spl
index="soc-splunk-lab" sourcetype="dns_logs"
| stats count dc(query) as unique_domains by source_ip
| sort - unique_domains
| head 10
```

### Purpose

Identify source IP addresses generating DNS requests to a high number of unique domains.

### Result

The query displayed the top 10 source IP addresses with the highest number of unique queried domains.  
This analysis helps identify potentially unusual DNS behavior.

---

## Long DNS Query Detection

```spl
index="soc-splunk-lab" sourcetype="dns_logs"
| eval query_length=len(query)
| where query_length > 50
| table _time source_ip query query_length
| sort - query_length
```

### Purpose

Identify unusually long DNS queries that may indicate abnormal DNS activity, encoded subdomains, or potential DNS tunneling behavior.

### Result

DNS queries with unusually long domain names were identified during the analysis.  
The reviewed events appeared consistent with legitimate DNS testing activity, and no clearly malicious behavior was observed in the current dataset.

### Screenshot

```text
screenshots/long-dns-queries.png
```

---

## Suspicious TLD Investigation

```spl
index="soc-splunk-lab" sourcetype="dns_logs"
| where match(query, "\.(xyz|top|club|info|ru)$")
| stats count by query
| sort - count
```

### Purpose

Identify DNS queries associated with potentially suspicious or uncommon top-level domains (TLDs), such as `.ru`, `.info`, `.xyz`, `.top`, and `.club`.

### Result

Two DNS queries matched the selected TLD patterns during the analysis.  
The domains were further investigated using external threat intelligence platforms, including VirusTotal and AbuseIPDB.  
One domain, `www.ironwarez.info`, was flagged as suspicious/malicious during enrichment analysis.

### Screenshots

```text
screenshots/suspicious-tlds.png
```

```text
screenshots/suspicious-tlds-VirusTotal.png
```

---

## Rare DNS Query Analysis

```spl
index="soc-splunk-lab" sourcetype="dns_logs"
| stats count by query
| where count=1
| sort query
```

### Purpose

Identify rare or low-frequency DNS queries that may indicate unusual activity, uncommon domains, or potential threat hunting opportunities.

### Result

Several low-frequency DNS queries were identified during the analysis.  
Among the observed domains were `update.utorrent.com` and `search.vuze.com`, which are associated with torrent/P2P software services.

These domains were later reviewed using external threat intelligence platforms for additional context.

### Screenshot

```text
screenshots/rare-dns-queries.png
```

---

## DNS Activity Over Time

```spl
index="soc-splunk-lab" sourcetype="dns_logs"
| rex field=_raw "^(?<unix_time>\d+\.\d+)"
| eval _time=unix_time
| timechart span=1m count as dns_events
```

### Purpose

Visualize DNS traffic activity over time in order to identify traffic spikes and overall DNS activity patterns throughout the captured dataset.

### Result

The analysis revealed multiple spikes in DNS traffic volume during the observed timeframe.  
The query also validated that event timestamps were successfully extracted and usable for time-based analysis within Splunk.

### Screenshot

```text
Dashboards/dns-activity-over-time-panel.png
```
