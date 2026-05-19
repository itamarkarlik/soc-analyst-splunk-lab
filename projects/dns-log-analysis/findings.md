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

---

## Finding 2 - P2P / Torrent-Related DNS Activity

### Description

During rare DNS query analysis, DNS requests associated with torrent/P2P-related services were identified within the dataset.

### Evidence

Observed domains:

```text
update.utorrent.com
search.vuze.com
```

Observed internal hosts:

```text
192.168.202.76
192.168.202.137
```

Observed activity:

- `192.168.202.76` generated DNS requests to:
  - `search.vuze.com`
  - `update.utorrent.com`

- `192.168.202.137` generated DNS requests to:
  - `update.utorrent.com`

### Investigation

The domains were reviewed using external threat intelligence platforms, including:

- VirusTotal
- AbuseIPDB

The reviewed domains were associated with torrent/P2P-related infrastructure and were flagged as suspicious or potentially unwanted by multiple sources.

### Conclusion

The investigation identified DNS activity related to torrent/P2P-associated services within the environment.  
While this does not confirm malicious activity, such traffic may indicate the use of unauthorized software or potentially unwanted applications.
