# {{ dbd_mysql_overview }}

This dashboard provides basic information about {{ mysql }} hosts.

## [MySQL Uptime](dashboard-mysql-overview.md#uptime)

The amount of time since the {{ mysql }} server process was started.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [Current QPS](dashboard-mysql-overview.md#current-qps)

Based on the queries reported by {{ mysql }}’s {{ sql_show_status }} command,
this metric shows the number of queries executed by the server during
the last second.n This metric includes statements executed within
stored programs.

This variable does not include the following commands:


* `COM_PING`


* `COM_STATISTICS`

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [InnoDB Buffer Pool Size](dashboard-mysql-overview.md#innodb-buffer-pool-size)

Absolute value of the InnoDB buffer pool used for caching data and indexes in
memory.

The goal is to keep the working set in memory. In most cases, this should be
between 60%-90% of available memory on a dedicated database host, but depends on
many factors.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [Buffer Pool Size % of Total RAM](dashboard-mysql-overview.md#buffer-poolsize-percentage-of-total-ram)

The ratio between {{ innodb }} buffer pool size and total memory.  In most cases, the
InnoDB buffer pool should be between 60% and 90% of available memory on a
dedicated database host, but it depends on many factors.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Connections](dashboard-mysql-overview.md#connections)

Max Connections

    The maximum permitted number of simultaneous client
    connections. This is the value of the `max_connections` variable.

Max Used Connections

    The maximum number of connections that have been in use simultaneously since
    the server was started.

Connections

    The number of connection attempts (successful or not) to the {{ mysql }} server.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Active Threads](dashboard-mysql-overview.md#active-threads)

Threads Connected

    The number of open connections.

Threads Running

    The number of threads not sleeping.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Questions](dashboard-mysql-overview.md#questions)

The number of queries sent to the server by clients, *excluding those executed
within stored programs*.

This variable does not count the following commands:

{{ view_all_metrics }} {{ dbd_mysql_overview }}


* COM_PING


* COM_STATISTICS


* COM_STMT_PREPARE


* COM_STMT_CLOSE


* COM_STMT_RESET

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Thread Cache](dashboard-mysql-overview.md#thread-cache)

The thread_cache_size metric informs how many threads the server should cache to
reuse. When a client disconnects, the client’s threads are put in the cache if
the cache is not full. It is autosized in {{ mysql }} 5.6.8 and above (capped to
100).

Requests for threads are satisfied by reusing threads taken from the cache if
possible, and only when the cache is empty is a new thread created.


* Threads_created: The number of threads created to handle connections.


* Threads_cached: The number of threads in the thread cache.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Select Types](dashboard-mysql-overview.md#select-types)

As with most relational databases, selecting based on indexes is more efficient
than scanning the data of an entire table. Here, we see the counters for selects
not done with indexes.


* *Select Scan* is how many queries caused full table scans, in which all the
data in the table had to be read and either discarded or returned.


* *Select Range* is how many queries used a range scan, which means {{ mysql }}
scanned all rows in a given range.


* *Select Full Join* is the number of joins that are not joined on an index,
this is usually a huge performance hit.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Sorts](dashboard-mysql-overview.md#sorts)

Due to a query’s structure, order, or other requirements, {{ mysql }} sorts the rows
before returning them. For example, if a table is ordered 1 to 10 but you want
the results reversed, {{ mysql }} then has to sort the rows to return 10 to 1.

This graph also shows when sorts had to scan a whole table or a given range of a
table in order to return the results and which could not have been sorted via an
index.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Slow Queries](dashboard-mysql-overview.md#slow-queries)

Slow queries are defined as queries being slower than the {{ opt_long_query_time }}
setting. For example, if you have {{ opt_long_query_time }} set to **3**, all
queries that take longer than **3** seconds to complete will show on this graph.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [Aborted Connections](dashboard-mysql-overview.md#aborted-connections)

When a given host connects to {{ mysql }} and the connection is interrupted in the
middle (for example due to bad credentials), {{ mysql }} keeps that info in a system
table (since 5.6 this table is exposed in performance_schema).

If the amount of failed requests without a successful connection reaches the
value of *max_connect_errors*, {{ mysqld }} assumes that something is wrong and
blocks the host from further connections.

To allow connections from that host again, you need to issue the
{{ sql_flush_hosts }} statement.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [Table Locks](dashboard-mysql-overview.md#table-locks)

{{ mysql }} takes a number of different locks for varying reasons. In this graph we
see how many Table level locks {{ mysql }} has requested from the storage engine. In
the case of {{ innodb }}, many times the locks could actually be row locks as it
only takes table level locks in a few specific cases.

It is most useful to compare {{ locks_immediate }} and {{ locks_waited }}. If
{{ locks_waited }} is rising, it means you have lock contention. Otherwise,
{{ locks_immediate }} rising and falling is normal activity.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Network Traffic](dashboard-mysql-overview.md#network-traffic)

This metric shows how much network traffic is generated by {{ mysql }}. *Outbound*
is network traffic sent from {{ mysql }} and *Inbound* is the network traffic that
{{ mysql }} has received.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Network Usage Hourly](dashboard-mysql-overview.md#network-usage-hourly)

This metric shows how much network traffic is generated by {{ mysql }} per
hour. You can use the bar graph to compare data sent by {{ mysql }} and data
received by {{ mysql }}.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Internal Memory Overview](dashboard-mysql-overview.md#internal-memory-overview)

This metric shows the various uses of memory within {{ mysql }}.

System Memory

> Total Memory for the system.

{{ innodb }} Buffer Pool Data

> {{ innodb }} maintains a storage area called the buffer pool for caching data and
> indexes in memory. Knowing how the {{ innodb }} buffer pool works, and taking
> advantage of it to keep frequently accessed data in memory, is an important
> aspect of {{ mysql }} tuning.

{{ tokudb }} Cache Size

> Similar in function to the {{ innodb }} Buffer Pool, {{ tokudb }} will allocate 50%
> of the installed RAM for its own cache. While this is optimal in most
> situations, there are cases where it may lead to memory over allocation. If
> the system tries to allocate more memory than is available, the machine will
> begin swapping and run much slower than normal.

Key Buffer Size

> Index blocks for {{ myisam }} tables are buffered and are shared by all
> threads. *key_buffer_size* is the size of the buffer used for index
> blocks. The key buffer is also known as the *key cache*.

Adaptive Hash Index Size

> The {{ innodb }} storage engine has a special feature called adaptive hash
> indexes. When InnoDB notices that some index values are being accessed very
> frequently, it builds a hash index for them in memory on top of B-Tree
> indexes. This allows for very fast hashed lookups.

Query Cache Size

> The query cache stores the text of a {{ sql_select }} statement together with the
> corresponding result that was sent to the client. The query cache has huge
> scalability problems in that only one thread can do an operation in the query
> cache at the same time. This serialization is true for {{ sql_select }} and also
> for {{ sql_insert }}, {{ sql_update }}, and {{ sql_delete }}. This also means that the
> larger the *query_cache_size* is set to, the slower those operations become.

{{ innodb }} Dictionary Size

> The data dictionary is {{ innodb }} internal catalog of tables. {{ innodb }} stores
> the data dictionary on disk, and loads entries into memory while the server
> is running. This is somewhat analogous to table cache of {{ mysql }}, but instead
> of operating at the server level, it is internal to the {{ innodb }} storage
> engine.

{{ innodb }} Log Buffer Size

> The {{ mysql }} {{ innodb }} log buffer allows transactions to run without having to
> write the log to disk before the transactions commit. The size of this buffer
> is configured with the *innodb_log_buffer_size* variable.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [Top Command Counters and Top Command Counters Hourly](dashboard-mysql-overview.md#top-command-counters.top-command-counters-hourly)

See [https://dev.mysql.com/doc/refman/5.7/en/server-status-variables.html#statvar_Com_xxx](https://dev.mysql.com/doc/refman/5.7/en/server-status-variables.html#statvar_Com_xxx)

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Handlers](dashboard-mysql-overview.md#handlers)

Handler statistics are internal statistics on how {{ mysql }} is selecting,
updating, inserting, and modifying rows, tables, and indexes.

This is in fact the layer between the Storage Engine and {{ mysql }}.


* *read_rnd_next* is incremented when the server performs a full table scan and
this is a counter you don’t really want to see with a high value.


* *read_key* is incremented when a read is done with an index.


* *read_next* is incremented when the storage engine is asked to ‘read the next
index entry’. A high value means a lot of index scans are being done.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## [MySQL Query Cache Memory and MySQL Query Cache Activity](dashboard-mysql-overview.md#query-cache-memory.query-cache-activity)

The query cache has huge scalability problems in that only one thread can do an
operation in the query cache at the same time. This serialization is true not
only for {{ sql_select }}, but also for {{ sql_insert }}, {{ sql_update }}, and
{{ sql_delete }}.

This also means that the larger the query_cache_size is set to, the slower
those operations become. In concurrent environments, the {{ mysql }} Query Cache
quickly becomes a contention point, decreasing performance. {{ mariadb }} and
{{ amazon_aurora }} have done work to try and eliminate the query cache contention
in their flavors of {{ mysql }}, while {{ mysql }} 8.0 has eliminated the query cache
feature.

The recommended settings for most environments is to set:

```
query_cache_type=0
query_cache_size=0
```

**NOTE**: While you can dynamically change these values, to completely remove the
contention point you have to restart the database.

{{ view_all_metrics }} {{ dbd_mysql_overview }}

## MySQL Open Tables, MySQL Table Open Cache Status, and MySQL Table Definition Cache [metric.mysql-table-definition-cache.mysql-open-cache-status.mysql-open-table]

The recommendation is to set the table_open_cache_instances to a loose
correlation to virtual CPUs, keeping in mind that more instances means the cache
is split more times. If you have a cache set to 500 but it has 10 instances,
each cache will only have 50 cached.

The table_definition_cache and table_open_cache can be left as default as
they are autosized {{ mysql }} 5.6 and above (do not set them to any value).

{{ view_all_metrics }} {{ dbd_mysql_overview }}

<!-- TODO: transform into foot references -->

---
