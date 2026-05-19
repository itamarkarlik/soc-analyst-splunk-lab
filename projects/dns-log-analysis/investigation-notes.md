# Field Extraction Validation

## DNS Log Structure Review

During the initial review of the raw DNS events, the log structure was manually analyzed in order to understand the position of important network fields within the dataset.

Based on the event structure, the following fields were identified:
- Source IP
- Source Port
- Destination IP
- Destination Port
- Protocol
- DNS Query

The review also showed that most DNS traffic was sent over destination port 53 using UDP.

## Destination Port Observation

Field statistics for the extracted `dest_port` field were reviewed directly within Splunk.  
Most observed traffic was associated with standard DNS port `53`, while additional activity involving ports `137`, `5355`, and `5353` was also identified.

# Timestamp Parsing

The original DNS logs contained Unix timestamp values within the raw event data.

The timestamps were extracted at search time using `rex` and converted into Splunk’s `_time` field using `eval` to support time-based analysis and visualization.
