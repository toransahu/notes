# GCP BigQuery

[TOC]

# Introduction

Provider managed, serverless, multi-cloud data warehouse.

# Dataset

# Table

## Row-level Security

https://cloud.google.com/bigquery/quotas#row_level_security

# BigQuery Storage Write API

https://cloud.google.com/bigquery/docs/write-api

- new, fast, cheaper, gRPC based API 
- suitable for both batch & stream loading


# Cost

## Data Ingestion (load jobs)
https://cloud.google.com/bigquery/pricing#data_ingestion_pricing

### Batch Loading
- load bulk data into one or more table
- free
- uses shared pool of slots
- option to purchase dedicated slots to run load jobs
    - flat-rate pricing
- no guarantee of availability/capacity

### Stream Loading (Legacy)
- load 1 row at a time (cost per successfull inserts)
- $0.01 per 200 MB
- each row is considered atleast 1KB

### Stream Loading (using BigQuery Storage Write API)
- $0.025 per 1 GB
- first 2 TB per month are free

## BigQuery Data Storage

https://cloud.google.com/bigquery/pricing#storage

- first 10 GB per month is free
- for more than 1PB, contact sales team for pricing
- pricing is prorated per MB, per second
    - i.e. 1 GB of Long-term storage for half month is $0.005
- If the table is edited, the price reverts back to the regular storage pricing, and the 90-day timer starts counting from zero

### Active Storage

- if a table[-partition] is modified for `<= 90` consecutive days
- $0.02 per GB

### Long-term Storage

- if a table[-partition] is NOT modified for `> 90` consecutive days
- pricing is ~50% half of Active Storage pricing
- $0.01 per GB

### Data Size Calculation
 
https://cloud.google.com/bigquery/pricing#data

- table size is calculated based on column data-type size
- when its in uncompressed form


## Data Fetch/Query/Extraction/Read/Export


# Quota & Limit

## Quota Error

https://cloud.google.com/docs/quota#quota_errors

 - rateLimitExceeded
     - This value indicates a short-term limit
     - To resolve these limit issues, retry the operation after few seconds
     - Use exponential backoff between retry attempts
        - That is, exponentially increase the delay between each retry
- quotaExceeded
    - This value indicates a longer-term limit
    - If you reach a longer-term quota limit, you should wait 10 minutes or longer before trying the operation again
    - If you consistently reach one of these longer-term quota limits, you should analyze your workload for ways to mitigate the issue
        - Mitigations can include optimizing your workload or requesting a quota increase

### Diagnosis

https://cloud.google.com/bigquery/docs/troubleshoot-quotas#diagnosis

e.g.

```sql
SELECT
 job_id,
 creation_time,
 error_result
FROM `region-us`.INFORMATION_SCHEMA.JOBS_BY_PROJECT
WHERE creation_time > TIMESTAMP_SUB(CURRENT_TIMESTAMP, INTERVAL 1 DAY) AND
      error_result.reason IN ('rateLimitExceeded', 'quotaExceeded')
```



### raise self._exception google.api_core.exceptions.Forbidden: 403 Exceeded rate limits: too many table update operations for this table. For more information, see https://cloud.google.com/bigquery/docs/troubleshoot-quotas

https://cloud.google.com/bigquery/docs/troubleshoot-quotas

## Datasets

https://cloud.google.com/bigquery/quotas#dataset_limits

- Maximum number of datasets: unlimited (per project)
- Number of tables per dataset: unlimited
    - When you use an API call, enumeration performance slows as you approach 50,000 tables in a dataset
    - The Cloud console can display up to 50,000 tables for each dataset
- Number of authorized resources in a dataset's access control list: 2500 resources

## Table

https://cloud.google.com/bigquery/quotas#table_limits

### Standard Table

https://cloud.google.com/bigquery/quotas#standard_tables

- Table operations per day: 1500
- Maximum number of columns per table: 10000

### Partitioned Table

https://cloud.google.com/bigquery/quotas#partitioned_tables

-  Number of partitions per partitioned table: 4000

## BigQuery API

https://cloud.google.com/bigquery/quotas#api_request_quotas

## load jobs (Bulk Load?)

https://cloud.google.com/bigquery/quotas#load_jobs

- Load jobs per day: 100000 jobs
    - i.e. 1.15 job per second
    - failed load jobs count toward this limit
- Maximum size per load job: 15 TB 
- Load job execution-time limit: 6 hours
    - A load job fails if it executes for longer than six hours
- CSV: Maximum file size 
    - compressed: 4 GB 
    - uncompressed: 5 TB 

NOTE: If regularly exceed the load job limits due to frequent updates, consider streaming data into BigQuery instead.

## streaming inserts (Legacy)

https://cloud.google.com/bigquery/quotas#streaming_inserts

- Maximum bytes per second per project 
    - in the us and eu multi-regions: 1 GB per second
    - in other region: 300 MB per second
- Maximum row size 	10 MB 
- HTTP request size limit 	10 MB
- Maximum rows per request 	50,000 rows

## streaming inserts (New Streaming Write API)

https://cloud.google.com/bigquery/quotas#write-api-limits

- Concurrent connections 	10,000 in multi-regions; 100 in regions 
- Pending stream bytes 	10 TB in multi-regions; 100 GB in regions
- Throughput 	3 GB per second throughput in multi-regions; 300 MB per second in regions
- CreateWriteStream requests 	30,000 streams every 4 hours, per project
- Batch commits 	10,000 streams per table
- Request size 	10 MB

## Monitoring Quota Metrics

https://cloud.google.com/docs/quota#monitoring_quota_metrics

# Partitioning

# Clients

## `python-bigquery`

https://github.com/googleapis/python-bigquery

- load_table_from_dataframe
    - uses CSV format by default
    - good performance for small batch

## `pandas-gbq`

https://github.com/googleapis/python-bigquery-pandas

- load_table_from_dataframe
    - uses parquet format by default


