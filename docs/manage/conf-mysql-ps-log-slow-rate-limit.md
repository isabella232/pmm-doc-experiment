# log_slow_rate_limit

The `log_slow_rate_limit` variable defines the fraction of queries captured by
the {{ slow_query_log }}.  A good rule of thumb is to have approximately 100 queries
logged per second.  For example, if your {{ percona_server }} instance processes
10_000 queries per second, you should set `log_slow_rate_limit` to `100` and
capture every 100th query for the {{ slow_query_log }}.

**NOTE**: When using query sampling, set `log_slow_rate_type` to `query`
so that it applies to queries, rather than sessions.

It is also a good idea to set `log_slow_verbosity` to `full`
so that maximum amount of information about each captured query
is stored in the slow query log.
