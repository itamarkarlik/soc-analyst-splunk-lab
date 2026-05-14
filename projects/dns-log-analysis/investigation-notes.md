# Field Extraction Validation

## Initial Extraction

An initial field extraction was created using the Splunk UI to identify the DNS `query` field.

## Validation Results

During validation, it was identified that the extracted field covered only part of the dataset.  
The total event count was significantly higher than the number of events containing the `query` field.

This indicated that some DNS log formats were not being parsed correctly by the extraction.

## Resolution

To improve parsing coverage and analysis accuracy, search-time extraction using `rex` was used for the main DNS analysis queries.
