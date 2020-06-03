# Query Response Time Plugin

Query response time distribution is a feature available in {{ percona_server }}.  It
provides information about changes in query response time for different groups
of queries, often allowing to spot performance problems before they lead to
serious issues.

To enable collection of query response time:


1. Install the {{ query_response_time }} plugins:

```
mysql> INSTALL PLUGIN QUERY_RESPONSE_TIME_AUDIT SONAME 'query_response_time.so';
mysql> INSTALL PLUGIN QUERY_RESPONSE_TIME SONAME 'query_response_time.so';
mysql> INSTALL PLUGIN QUERY_RESPONSE_TIME_READ SONAME 'query_response_time.so';
mysql> INSTALL PLUGIN QUERY_RESPONSE_TIME_WRITE SONAME 'query_response_time.so';
```


2. Set the global varible {{ opt_query_response_time_stats }} to `ON`:

```
mysql> SET GLOBAL query_response_time_stats=ON;
```
