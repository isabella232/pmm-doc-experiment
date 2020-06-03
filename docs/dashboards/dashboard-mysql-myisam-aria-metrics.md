# {{ mysql }} {{ myisam }} {{ aria }} Metrics Dashboard

The {{ mysql }} {{ myisam }} {{ aria }} Metrics dashboard describes the specific features
of {{ mariadb }} MySQL server: [Aria storage engine](https://mariadb.com/kb/en/the-mariadb-library/aria-storage-engine/), [Online DDL (online alter table)](https://mariadb.com/kb/en/the-mariadb-library/alter-table/),

> and [InnoDB defragmentation patch](https://mariadb.com/kb/en/the-mariadb-library/defragmenting-innodb-tablespaces/). This dashboard contains the following metrics:

## {{ aria }} Storage Engine

Aria storage is specific for {{ mariadb }} Server. Aria has most of the same
variables that {{ myisam }} has, but with an {{ aria }} prefix. If you use {{ aria }}
instead of {{ myisam }}, then you should make {{ opt_key_buffer_size }} smaller and
aria-pagecache-buffer-size bigger.

## {{ aria }} Pagecache Reads/Writes

This graph is similar to InnoDB buffer pool reads and
writes. {{ opt_aria_pagecache_buffer_size }} is the main cache for aria storage
engine. If you see high reads and writes (physical IO), i.e. reads is close to
read requests or writes are close to write requests you may need to increase the
{{ opt_aria_pagecache_buffer_size }} (you may need to decrease other buffers:
{{ opt_key_buffer_size }}, {{ opt_innodb_buffer_pool_size }} etc)

## {{ aria }} Pagecache Blocks

This graphs shows the utilization for the aria pagecache.  This is similar to
{{ innodb }} buffer pool graph. If you see all blocks are used you may consider
increasing {{ opt_aria_pagecache_buffer_size }} (you may need to decrease other
buffers: {{ opt_key_buffer_size }}, {{ opt_innodb_buffer_pool_size }} etc)

## {{ aria }} Transactions Log Syncs

This metric is similar to {{ innodb }} log file syncs. If you see lots of log syncs
and want to relax the durability settings you can change (in seconds) from 30
(default) to a higher number. It is good to look at the disk IO dashboard as
well.
