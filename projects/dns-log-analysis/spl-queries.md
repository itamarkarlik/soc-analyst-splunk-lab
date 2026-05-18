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

## Top Queried DNS Domains

```spl
index="soc-splunk-lab" sourcetype="dns_logs" port=53
| rex field=_raw "^(?:\S+\s+){8}(?<dns_query>\S+)"
| search dns_query!="*.in-addr.arpa"
| stats count by dns_query
| sort - count
| head 10
```

### Purpose
Extract DNS query domains from raw DNS logs and identify the most frequently requested domains in the dataset.

### Result
The query successfully extracted DNS query domains into a searchable field and enabled frequency analysis across the dataset.

Top observed domains:
- `teredo.ipv6.microsoft.com`
- `tools.google.com`
- `www.apple.com`
- `time.apple.com`
- `safebrowsing.clients.google.com`

### Notes
The DNS query field was extracted from raw events using `rex` because the initial Splunk UI field extraction did not provide reliable coverage across the full dataset.

### Screenshot
`screenshots/dns-query-extraction-results.png`
`screenshots/top-queried-domains-dashboard.png`
