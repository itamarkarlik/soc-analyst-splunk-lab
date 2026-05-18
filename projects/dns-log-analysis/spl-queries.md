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
