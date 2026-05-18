# Field Extraction Validation

## DNS Log Structure Review

During the initial review of the raw DNS events, the log structure was manually analyzed in order to understand the position of important network fields within the dataset.

Based on the event structure, the following fields were identified:
- Source IP
- Source Port
- Destination IP
- Destination Port
- Protocol

The review also showed that most DNS traffic was sent over destination port 53 using UDP.

## Initial Extraction

An initial field extraction was created using the Splunk UI to identify the DNS `query` field.

## Validation Results

During validation, it was identified that the extracted field covered only part of the dataset.  
The total event count was significantly higher than the number of events containing the `query` field.

This indicated that some DNS log formats were not being parsed correctly by the extraction.

## Resolution

To improve parsing coverage and analysis accuracy, search-time extraction using `rex` was used for the main DNS analysis queries.
