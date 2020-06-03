# {{ mysql }} Query Response Time

This dashboard provides information about query response time distribution.

## [Average Query Response Time](dashboard-mysql-query-response-time.md#average)

The Average Query Response Time graph shows information collected using
the Response Time Distribution plugin sourced from table
*INFORMATION_SCHEMA.QUERY_RESPONSE_TIME*. It computes this value across all
queries by taking the sum of seconds divided by the count of seconds.

{{ view_all_metrics }} {{ mysql }} Query Response Time

## [Query Response Time Distribution](dashboard-mysql-query-response-time.md#distribution)

Shows how many fast, neutral, and slow queries are executed per second.

Query response time counts (operations) are grouped into three buckets:


* 100ms - 1s


* 1s - 10s


* > 10s

{{ view_all_metrics }} {{ mysql }} Query Response Time

## [Average Query Response Time (Read/Write Split)](dashboard-mysql-query-response-time.md#average-read-write-split)

Available only in {{ percona }} Server for {{ mysql }}, this metric provides
visibility of the split of READ vs WRITE query response time.

{{ view_all_metrics }} {{ mysql }} Query Response Time

## [Read Query Response Time Distribution](dashboard-mysql-query-response-time.md#read-distribution)

Available only in Percona Server for MySQL, illustrates READ query response time
counts (operations) grouped into three buckets:


* 100ms - 1s


* 1s - 10s


* > 10s

{{ view_all_metrics }} {{ mysql }} Query Response Time

## [Write Query Response Time Distribution](dashboard-mysql-query-response-time.md#write-distribution)

Available only in Percona Server for MySQL, illustrates WRITE query response
time counts (operations) grouped into three buckets:


* 100ms - 1s


* 1s - 10s


* > 10s

{{ view_all_metrics }} {{ mysql }} Query Response Time
