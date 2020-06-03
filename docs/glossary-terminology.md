# Terminology Reference

## A TEST TITLE

Some test content

## [Data retention](glossary-terminology.md#data-retention)

> By default, {{ prometheus }} stores time-series data for 30 days,
> and QAN stores query data for 8 days.

> Depending on available disk space and your requirements, you may
> need to adjust data retention time.

> You can control data retention via the *Settings* dashboard.

## [Data Source Name](glossary-terminology.md#data-source-name)

> A database server attribute found on the QAN page. It informs how
> PMM connects to the selected database.

## [DSN](glossary-terminology.md#dsn)

> See Data Source Name

## [Grand Total Time](glossary-terminology.md#grand-total-time)

> Grand Total Time.(percent of grand total time) is the percentage
> of time that the database server spent running a specific query,
> compared to the total time it spent running all queries during
> the selected period of time.

## [%GTT](glossary-terminology.md#gtt)

> See Grand Total Time

## [External Monitoring Service](glossary-terminology.md#external-monitoring-service)

> A monitoring service which is not provided by PMM directly. It is
> bound to a running {{ prometheus }} exporter. As soon as such an service is
> added, you can set up the Metrics Monitor
> to display its graphs.

## [Metrics](glossary-terminology.md#metrics)

> A series of data which are visualized in {{ pmm }}.

## [Metrics Monitor (MM)](glossary-terminology.md#metrics-monitor)

> Component of PMM Server that provides a historical view of
> metrics critical to a {{ mysql }} server instance.

## [Monitoring service](glossary-terminology.md#monitoring-service)

> A special service which collects information from the database instance
> where PMM Client is installed.

> To add a monitoring service, use the **pmm-admin add** command.

## [PMM](glossary-terminology.md#pmm)

> Percona Monitoring and Management

## [pmm-admin](glossary-terminology.md#pmm-admin)

> A program which changes the configuration of the PMM Client. See
> detailed documentation in the pmm-admin section.

## [PMM Client](glossary-terminology.md#pmm-client)

> Collects {{ mysql }} server metrics, general system metrics,
> and query analytics data for a complete performance overview.

> The collected data is sent to PMM Server.

> For more information, see Client/Server Architecture - an Overview.

## [PMM Docker Image](glossary-terminology.md#pmm-docker-image)

> A docker image which enables installing the {{ pmm_server }} by
> using **docker**.

## [PMM Home Page](glossary-terminology.md#pmm-home-page)

> The starting page of the PMM portal from which you can have an overview of your environment, open the tools of
> PMM, and browse to online resources.

> On the {{ pmm }} home page, you can also find the version number and a button to
> update your {{ pmm_server }} (see PMM Version).

## [PMM Server](glossary-terminology.md#pmm-server)

> Aggregates data collected by PMM Client and presents it in the
> form of tables, dashboards, and graphs in a web interface.

> {{ pmm_server }} combines the backend API and storage for collected data with
> a frontend for viewing time-based graphs and performing thorough analysis
> of your {{ mysql }} and {{ mongodb }} hosts through a web interface.

> Run {{ pmm_server }} on a host that you will use to access this data.

## [PMM Server Version](glossary-terminology.md#pmm-server-version)

> If PMM Server is installed via {{ docker }}, you can check
> the current {{ pmm_server }} version by running {{ docker_exec }}:

> {{ tip_run_this_root }}

> ```
> $ docker exec -it pmm-server head -1 /srv/update/main.yml
> # v1.5.3
> ```

## [PMM user permissions for AWS](glossary-terminology.md#pmm-user-permissions-for-aws)

> When creating a [IAM user](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_SettingUp.html#CHAP_SettingUp.IAM)
> for {{ amazon_rds }} DB instance that you intend to monitor in PMM, you need to set all
> required permissions properly. For this, you may copy the following {{ json }} for your
> IAM user:

> ```
> { "Version": "2012-10-17",
>   "Statement": [{ "Sid": "Stmt1508404837000",
>                   "Effect": "Allow",
>                   "Action": [ "rds:DescribeDBInstances",
>                               "cloudwatch:GetMetricStatistics",
>                               "cloudwatch:ListMetrics"],
>                               "Resource": ["*"] },
>                  { "Sid": "Stmt1508410723001",
>                    "Effect": "Allow",
>                    "Action": [ "logs:DescribeLogStreams",
>                                "logs:GetLogEvents",
>                                "logs:FilterLogEvents" ],
>                                "Resource": [ "arn:aws:logs:*:*:log-group:RDSOSMetrics:*" ]}
>                ]
> }
> ```

## [PMM Version](glossary-terminology.md#pmm-version)

> The version of PMM appears at the bottom of the PMM server home page.

## [QAN](glossary-terminology.md#qan)

> See Query Analytics (QAN)

## [Query Analytics (QAN)](glossary-terminology.md#auery-analytics)

> Component of PMM Server that enables you to analyze
> {{ mysql }} query performance over periods of time.

## [Query Load](glossary-terminology.md#query-load)

> The percentage of time that the {{ mysql }} server spent executing a specific query.

## [Query Metrics Summary Table](glossary-terminology.md#query-metrics-summary-table)

> An element of Query Analytics (QAN) which displays the available
> metrics for the selected query.

## [Query Metrics Table](glossary-terminology.md#query-metrics-table)

> A tool within QAN which lists metrics applicable to the query
> selected in the query summary table.

## [Query Summary Table](glossary-terminology.md#query-summary-table)

> A tool within QAN which lists the queries which were run
> on the selected database server during the selected time
> or date range.

## [Quick ranges](glossary-terminology.md#quick-ranges)

> Predefined time periods which are used by QAN to collect metrics
> for queries. The following quick ranges are available:


> * last hour


> * last three hours


> * last five hours


> * last twelve hours


> * last twenty four hours


> * last five days

## [Selected Time or Date Range](glossary-terminology.md#selected-time-or-date-range)

> A predefined time period (see Quick ranges), such as 1 hour, or a
> range of dates that QAN uses to collects metrics.

## [Telemetry](glossary-terminology.md#telemetry)

> {{ percona }} may collect some **anonymous** statistics about the machine
> where {{ pmm }} is running.

> Currently, only the following information is gathered:


> * PMM Version,


> * Installation Method (Docker, AMI, OVF),


> * the Uptime,


> * {{ pmm_server }} unique ID.

> You may find here more details about what and how information is gathered,
> and how to disable telemetry on the *Settings* dashboard, if needed.

## [Version](glossary-terminology.md#version)

> A database server attribute found on the QAN page. it informs the
> full version of the monitored database server, as well as the product
> name, revision and release number.
