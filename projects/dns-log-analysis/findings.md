# Findings

## Dataset Overview

The DNS dataset contains 422,130 events successfully ingested into Splunk.

## Index Information

- Index: soc-splunk-lab
- Sourcetype: dns_logs

## Analysis Notes

This confirms successful log ingestion and validates that the dataset is ready for further DNS analysis and threat hunting activities.

---

## Finding 1 - Suspicious DNS Activity

### Description
During DNS traffic analysis, queries to uncommon top-level domains were identified.  

### Investigation
The domains were reviewed using external threat intelligence platforms, including:

- VirusTotal
- AbuseIPDB

The domain `www.ironwarez.info` was flagged as malicious/suspicious during enrichment analysis.

Additional DNS investigation revealed repeated DNS requests originating from the internal host:

```text
192.168.202.136
```

The activity included multiple `A` and `AAAA` DNS queries and repeated `NXDOMAIN` responses.

### Evidence

Observed domain:

```text
www.ironwarez.info
```

Observed internal host:

```text
192.168.202.136
```
### Screenshot

```text
screenshots/domain-tld-activity.png
```

### Conclusion
The investigation identified repeated DNS activity involving a domain flagged as malicious by external threat intelligence sources.  
While no direct evidence of compromise was confirmed, the observed activity was considered potentially suspicious and relevant for further monitoring.
