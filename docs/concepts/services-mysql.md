# MySQL requirements

{{ pmm }} supports all commonly used variants of {{ mysql }}, including
{{ percona_server }}, {{ mariadb }}, and {{ amazon_rds }}.  To prevent data loss and
performance issues, {{ pmm }} does not automatically change {{ mysql }} configuration.
However, there are certain recommended settings that help maximize monitoring
efficiency. These recommendations depend on the variant and version of {{ mysql }}
you are using, and mostly apply to very high loads.

{{ pmm }} can collect query data either from the {{ slow_query_log }} or from
{{ performance_schema }}.  The {{ slow_query_log }} provides maximum details, but can
impact performance on heavily loaded systems. On {{ percona_server }} the query
sampling feature may reduce the performance impact.

{{ performance_schema }} is generally better for recent versions of other {{ mysql }}
variants. For older {{ mysql }} variants, which have neither sampling, nor
{{ performance_schema }}, configure logging only slow queries.

**NOTE**: {{ mysql }} with too many tables can lead to PMM Server overload due to the
streaming of too much time series data. It can also lead to too many queries
from `mysqld_exporter` causing extra load on {{ mysql }}. Therefore PMM Server
disables most consuming `mysqld_exporter` collectors automatically if
there are more than 1000 tables.

You can add configuration examples provided below to `my.cnf` and
restart the server or change variables dynamically using the following syntax:

```
SET GLOBAL <var_name>=<var_value>
```

The following sample configurations can be used depending on the variant and
version of {{ mysql }}:


* If you are running {{ percona_server }} (or {{ xtradb_cluster }}), configure the
{{ slow_query_log }} to capture all queries and enable sampling. This will
provide the most amount of information with the lowest overhead.

```
log_output=file
slow_query_log=ON
long_query_time=0
log_slow_rate_limit=100
log_slow_rate_type=query
log_slow_verbosity=full
log_slow_admin_statements=ON
log_slow_slave_statements=ON
slow_query_log_always_write_time=1
slow_query_log_use_global_control=all
innodb_monitor_enable=all
userstat=1
```


* If you are running {{ mysql }} 5.6+ or {{ mariadb }} 10.0+, configure
Configuring Performance Schema.

```
innodb_monitor_enable=all
performance_schema=ON
```


* If you are running {{ mysql }} 5.5 or {{ mariadb }} 5.5, configure logging only slow
queries to avoid high performance overhead.

**NOTE**: This may affect the quality of monitoring data gathered by
{{ abbr_qan }}.

```
log_output=file
slow_query_log=ON
long_query_time=0
log_slow_admin_statements=ON
log_slow_slave_statements=ON
```

## [Creating a MySQL User Account to Be Used with PMM](services-mysql.md#pmm-conf-mysql-user-account-creating)

When adding a {{ mysql }} instance to monitoring, you can specify the {{ mysql }}
server superuser account credentials.  However, monitoring with the superuser
account is not advised. It’s better to create a user with only the necessary
privileges for collecting data.

As an example, the user `pmm` can be created manually with the necessary
privileges and pass its credentials when adding the instance.

To enable complete {{ mysql }} instance monitoring, a command similar to the
following is recommended:

<pre class="highlight"><style type="text/css">
span.prompt1:before {
  content: "$ ";
}
</style><span class="prompt1">sudo pmm-admin add mysql --username pmm --password &lt;password&gt;</span>
</pre>\\begin{Verbatim}[commandchars=\\\\\\{\\}]
$ sudo pmm-admin add mysql --username pmm --password <password>
\\end{Verbatim}Of course this user should have necessary privileges for collecting data. If
the `pmm` user already exists, you can grant the required privileges as
follows:

```
CREATE USER 'pmm'@'localhost' IDENTIFIED BY 'pass' WITH MAX_USER_CONNECTIONS 10;
GRANT SELECT, PROCESS, SUPER, REPLICATION CLIENT, RELOAD ON *.* TO 'pmm'@'localhost';
GRANT SELECT ON performance_schema.* TO 'pmm'@'localhost';
```

For more information, run:
{{ pmm_admin_add }}
{{ opt_mysql }}
{{ opt_help }}
