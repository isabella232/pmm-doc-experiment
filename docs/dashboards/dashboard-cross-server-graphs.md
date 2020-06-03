# Cross Server Graphs

## Load Average

This metric is the average number of processes that are either in a runnable or
uninterruptable state.  A process in a runnable state is either using the CPU or
waiting to use the CPU.  A process in uninterruptable state is waiting for some
I/O access, eg waiting for disk.

This metric is best used for trends. If you notice the load average rising, it
may be due to innefficient queries. In that case, you may further analyze your
queries in QAN.

{{ view_all_metrics }} Cross Server Graphs

## {{ mysql }} Queries

This metric is based on the queries reported by the {{ mysql }} command
{{ sql_show_status }}. It shows the average number of statements executed by the
server. This variable includes statements executed within stored programs,
unlike the {{ opt_questions }} variable. It does not count *COM_PING* or
*COM_STATISTICS* commands.

{{ view_all_metrics }} Cross Server Graphs

## {{ mysql }} Traffic

This metric shows the network traffic used by the {{ mysql }} process.

{{ view_all_metrics }} Cross Server Graphs
