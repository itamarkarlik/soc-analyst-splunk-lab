# Total DNS Event Count

```spl
index="soc-splunk-lab" sourcetype="dns_logs"
| stats count
```
## Purpose:
Count the total number of DNS events in the dataset.

## Result:
422,130 DNS events were identified.

### Screenshot
`screenshots/event-count.png`

---

## Top Queried Domains

```spl
index="soc-splunk-lab" sourcetype=dns_logs
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
`Dashboards/top-queried-domains-dashboard.png`

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
`Dashboards/top-source-ip.png`


## Unique Queried Domains by Source IP

```spl
index="soc-splunk-lab" sourcetype="dns_logs"
| stats count dc(dns_query) as unique_domains by src_ip
| sort - unique_domains
| head 10
```

### Purpose
Identify source IP addresses generating DNS requests to a high number of unique domains.

### Result
The query displayed the top 10 source IP addresses with the highest number of unique queried domains.  
This analysis helps identify potentially unusual DNS behavior.

## Long DNS Query Detection

```spl
index="soc-splunk-lab" sourcetype="dns_logs"
| eval query_length=len(dns_query)
| where query_length > 50
| table _time src_ip dns_query query_length
| sort - query_length
```

### Purpose
Identify unusually long DNS queries that may indicate abnormal DNS activity, encoded subdomains, or potential DNS tunneling behavior.

### Result
DNS queries with unusually long domain names were identified during the analysis.  
The reviewed events appeared consistent with legitimate DNS testing activity and no clearly malicious behavior was observed in the current dataset.

### Screenshot
```
screenshots/long-dns-queries.png
```
