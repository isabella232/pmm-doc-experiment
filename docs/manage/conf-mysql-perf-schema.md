# Configuring Performance Schema

The default source of query data for {{ pmm }} is the {{ slow_query_log }}.  It is
available in {{ mysql }} 5.1 and later versions.  Starting from {{ mysql }} 5.6
(including {{ percona_server }} 5.6 and later), you can choose to parse query data
from the {{ perf_schema }} instead of {{ slow_query_log }}.  Starting from {{ mysql }}
5.6.6, {{ perf_schema }} is enabled by default.

{{ perf_schema }} is not as data-rich as the {{ slow_query_log }}, but it has all the
critical data and is generally faster to parse. If you are not running
{{ percona_server }} (which supports sampling for the slow query log), then {{ performance_schema }} is a better alternative.

**NOTE**: Use of the performance schema is off by default in MariaDB 10.x.

To use {{ perf_schema }}, set the `performance_schema` variable to `ON`:

```
mysql> SHOW VARIABLES LIKE 'performance_schema';
+--------------------+-------+
| Variable_name      | Value |
+--------------------+-------+
| performance_schema | ON    |
+--------------------+-------+
```

If this variable is not set to **ON**, add the the following lines to the
{{ mysql }} configuration file {{ my_cnf }} and restart {{ mysql }}:

```
[mysql]
performance_schema=ON
```

If you are running a custom Performance Schema configuration, make sure that the
`statements_digest` consumer is enabled:

```
mysql> select * from setup_consumers;
+----------------------------------+---------+
| NAME                             | ENABLED |
+----------------------------------+---------+
| events_stages_current            | NO      |
| events_stages_history            | NO      |
| events_stages_history_long       | NO      |
| events_statements_current        | YES     |
| events_statements_history        | YES     |
| events_statements_history_long   | NO      |
| events_transactions_current      | NO      |
| events_transactions_history      | NO      |
| events_transactions_history_long | NO      |
| events_waits_current             | NO      |
| events_waits_history             | NO      |
| events_waits_history_long        | NO      |
| global_instrumentation           | YES     |
| thread_instrumentation           | YES     |
| statements_digest                | YES     |
+----------------------------------+---------+
15 rows in set (0.00 sec)
```

If the instance is already running, configure the {{ qan }} agent to collect data
from {{ perf_schema }}:


1. Open the {{ qan_name }} dashboard.


2. Click the {{ gui_settings }} button.


3. Open the {{ gui_settings }} section.


4. Select {{ opt_performance_schema }} in the {{ gui_collect_from }} drop-down list.


5. Click {{ gui_apply }} to save changes.

If you are adding a new monitoring instance with the {{ pmm_admin }} tool, use the
{{ opt_query_source }} *perfschema* option:

{{ tip_run_this_root }}

```
pmm-admin add mysql --username=pmm --password=pmmpassword --query-source='perfschema' ps-mysql 127.0.0.1:3306
```

For more information, run
{{ pmm_admin_add }}
{{ opt_mysql }}
{{ opt_help }}.
