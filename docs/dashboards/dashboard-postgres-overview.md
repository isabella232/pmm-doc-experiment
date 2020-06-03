# {{ dbd_postgres_overview }}

This dashboard provides basic information about {{ postgresql }} hosts.

## [Connected](dashboard-postgres-overview.md#connected)

Reports whether PMM Server can connect to the {{ postgresql }} instance.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Version](dashboard-postgres-overview.md#version)

The version of the {{ postgresql }} instance.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Shared Buffers](dashboard-postgres-overview.md#shared-buffers)

Defines the amount of memory the database server uses for shared memory
buffers. Default is `128MB`. Guidance on tuning is `25%` of RAM, but
generally doesn’t exceed `40%`.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Disk-Page Buffers](dashboard-postgres-overview.md#disk-page-buffers)

The setting `wal_buffers` defines how much memory is used for caching the
write-ahead log entries. Generally this value is small (`3%` of
`shared_buffers` value), but it may need to be modified for heavily loaded
servers.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Memory Size for each Sort](dashboard-postgres-overview.md#memory-size-for-each-sort)

The parameter work_mem defines the amount of memory assigned for internal sort
operations and hash tables before writing to temporary disk files. The default
is `4MB`.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Disk Cache Size](dashboard-postgres-overview.md#disk-cache-size)

{{ postgresql }}’s `effective_cache_size` variable tunes how much RAM you expect
to be available for disk caching. Generally adding Linux free+cached will give
you a good idea. This value is used by the query planner whether plans will fit
in memory, and when defined too low, can lead to some plans rejecting certain
indexes.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Autovacuum](dashboard-postgres-overview.md#autovacuum)

Whether autovacuum process is enabled or not. Generally the solution is to
vacuum more often, not less.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [PostgreSQL Connections](dashboard-postgres-overview.md#connections)

Max Connections

    The maximum number of client connections allowed. Change this value with
    care as there are some memory resources that are allocated on a per-client
    basis, so setting `max_connections` higher will generally increase overall
    {{ postgresql }} memory usage.

Connections

    The number of connection attempts (successful or not) to the {{ postgresql }}
    server.

Active Connections

    The number of open connections to the {{ postgresql }} server.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [PostgreSQL Tuples](dashboard-postgres-overview.md#tuples)

Tuples

    The total number of rows processed by {{ postgresql }} server: fetched, returned,
    inserted, updated, and deleted.

Read Tuple Activity

    The number of rows read from the database: as returned so fetched ones.

Tuples Changed per 5min

    The number of rows changed in the last 5 minutes: inserted, updated, and
    deleted ones.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [PostgreSQL Transactions](dashboard-postgres-overview.md#transactions)

Transactions

    The total number of transactions that have been either been committed or
    rolled back.

Duration of Transactions

    Maximum duration in seconds any active transaction has been running.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Temp Files](dashboard-postgres-overview.md#temp-files)

Number of Temp Files

    The number of temporary files created by queries.

Size of Temp files

    The total amount of data written to temporary files by queries in bytes.

**NOTE**: All temporary files are taken into account by these two gauges,
regardless of why the temporary file was created (e.g., sorting or hashing),
and regardless of the `log_temp_files` setting.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Conflicts and Locks](dashboard-postgres-overview.md#conflicts-and-locks)

Conflicts/Deadlocks

    The number of queries canceled due to conflicts with recovery in the database
    (due to dropped tablespaces, lock timeouts, old snapshots, pinned buffers,
    or deadlocks).

Number of Locks

    The number of deadlocks detected by {{ postgresql }}.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Buffers and Blocks Operations](dashboard-postgres-overview.md#buffers-and-blocks-operations)

Operations with Blocks

    The time spent reading and writing data file blocks by backends, in
    milliseconds.

**NOTE**: Capturing read and write time statistics is possible only if
`track_io_timing` setting is enabled. This can be done either in
configuration file or with the following query executed on the running
system:

```
ALTER SYSTEM SET track_io_timing=ON;
SELECT pg_reload_conf();
```

Buffers

    The number of buffers allocated by {{ postgresql }}.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Canceled Queries](dashboard-postgres-overview.md#canceled-queries)

The number of queries that have been canceled due to dropped tablespaces, lock
timeouts, old snapshots, pinned buffers, and deadlocks.

**NOTE**: Data shown by this gauge are based on the
`pg_stat_database_conflicts` view.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Cache Hit Ratio](dashboard-postgres-overview.md#cache-hit-ratio)

The number of times disk blocks were found already in the buffer cache, so that
a read was not necessary.

**NOTE**: This only includes hits in the {{ postgresql }} buffer cache, not the
operating system’s file system cache.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [Checkpoint Stats](dashboard-postgres-overview.md#checkpoint-stats)

The total amount of time that has been spent in the portion of checkpoint
processing where files are either written or synchronized to disk,
in milliseconds.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [PostgreSQL Settings](dashboard-postgres-overview.md#postgresql-settings)

The list of all settings of the {{ postgresql }} server.

{{ view_all_metrics }} {{ dbd_postgres_overview }}

## [System Summary](dashboard-postgres-overview.md#system-summary)

This section contains the following system parameters of the {{ postgresql }}
server: CPU Usage, CPU Saturation and Max Core Usage, Disk I/O Activity, and
Network Traffic.

{{ view_all_metrics }} {{ dbd_postgres_overview }}
