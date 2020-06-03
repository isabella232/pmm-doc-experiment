# Frequently Asked Questions

## How can I contact the developers?

The best place to discuss PMM with developers and other community members
is the [community forum](https://www.percona.com/forums/questions-discussions/percona-monitoring-and-management).

If you would like to report a bug,
use the [PMM project in JIRA](https://jira.percona.com/projects/PMM).

## What are the minimum system requirements for PMM?

### {{ pmm_server }}

Any system which can run Docker version 1.12.6 or later.

It needs roughly 1 GB of storage for each monitored database node
with data retention set to one week.

**NOTE**: By default, retention is set to 30 days for
Metrics Monitor and for Query Analytics.  Also consider
disabling table statistics, which can
greatly decrease Prometheus database size.

Minimum memory is 2 GB for one monitored database node, but it is not
linear when you add more nodes.  For example, data from 20 nodes
should be easily handled with 16 GB.

### {{ pmm_client }}

Any modern 64-bit Linux distribution. It is tested on the latest
versions of Debian, Ubuntu, CentOS, and Red Hat Enterprise Linux.

Minimum 100 MB of storage is required for installing the {{ pmm_client }}
package.  With good constant connection to {{ pmm_server }}, additional
storage is not required.  However, the client needs to store any
collected data that it is not able to send over immediately, so
additional storage may be required if connection is unstable or
throughput is too low.

## How to control data retention for PMM?

By default, both {{ prometheus }} and QAN store time-series data for 30 days.

Depending on available disk space and your requirements,
you may need to adjust data retention time.

You can control data retention by the following way.


1. Select the {{ pmm_settings }} dashboard in the main menu.


2. In the *Settings* section, enter new data retention value in days.


3. Click the *Apply changes* button.

## How often are nginx logs in PMM Server rotated?

{{ pmm_server }} runs `logrotate` to rotate nginx logs on a daily basis
and keep up to 10 latest log files.

## What privileges are required to monitor a {{ mysql }} instance?

See Creating a MySQL User Account to Be Used with PMM.

## Can I monitor multiple service instances?

Yes, you can add multiple instances of {{ mysql }} or some other service to be
monitored from one {{ pmm_client }}. In this case, you will need to provide a
distinct port and socket for each instance, and specify a unique name for each
instance (by default, it uses the name of the {{ pmm_client }} host).

For example, if you are adding complete MySQL monitoring for two local {{ mysql }}
servers, the commands could look similar to the following:

```
$ sudo pmm-admin add mysql --username root --password root instance-01 127.0.0.1:3001
$ sudo pmm-admin add mysql --username root --password root instance-02 127.0.0.1:3002
```

For more information, run

```
$ pmm-admin add mysql --help
```

## Can I rename instances?

You can remove any monitoring instance as described in Removing monitoring services with pmm-admin remove
and then add it back with a different name.

When you remove a monitoring service, previously collected data remains
available in {{ grafana }}.  However, the metrics are tied to the instance name.  So
if you add the same instance back with a different name, it will be considered a
new instance with a new set of metrics.  So if you are re-adding an instance and
want to keep its previous data, add it with the same name.

## Can I add an AWS RDS MySQL or Aurora MySQL instance from a non-default AWS partition?

By default the RDS discovery works with the default `aws` partition. But you
can switch to special regions, like the [GovCloud](https://aws.amazon.com/ru/govcloud-us/) one, with the alternative [AWS partitions](https://docs.aws.amazon.com/sdk-for-go/api/aws/endpoints/#pkg-constants) (e.g. `aws-us-gov`) adding them to the *Settings* via the [PMM Server API](https://www.percona.com/doc/percona-monitoring-and-management/2.x/manage/server-pmm-api.html):

You can specify any of them instead of the `aws` default value, or use several
of them, with the JSON Array  syntax: `["aws", "aws-cn"]`.

## How to troubleshoot communication issues between PMM Client and PMM Server?

Broken network connectivity may be caused by rather wide set of reasons.
Particularly, when using Docker, the container is
constrained by the host-level routing and firewall rules. For example, your
hosting provider might have default *iptables* rules on their hosts that block
communication between {{ pmm_server }} and {{ pmm_client }}, resulting in *DOWN* targets
in Prometheus. If this happens, check firewall and routing settings on the
Docker host.

Also {{ pmm }} is able to generate a set of diagnostics data which can be examined
and/or shared with Percona Support to solve an issue faster. You can get
collected logs from PMM Client using the `pmm-admin summary` command.

The logs archive obtained in this way includes PMM Client logs and also logs
which were received from the PMM Server, stored separately in the `client`
and `server` folders. The `server` folder also contains its own
`client` subfolder with the self-monitoring client information collected on
the PMM Server.

**NOTE**: Starting from PMM 2.4.0 there is an additional flag that allows to
fetch [pprof](https://github.com/google/pprof) debug profiles and add them
to the diagnostics data. To do it, run `pmm-admin summary --pprof`.

Obtaining logs from PMM Server can be done by specifying the
\`\`https://<address-of-your-pmm-server>/logs.zip\` URL, or by clicking
the `server logs` link on the [Prometheus dashboard](https://www.percona.com/doc/percona-monitoring-and-management/2.x/dashboards/dashboard-prometheus.html):



![image](/_images/get-logs-from-prometheus-dashboard.png)

The logs archive obtained in this way includes diagnostics information gathered
from the PMM Server, and the `client` subfolder with the self-monitoring
client information collected on the PMM Server.

## What resolution is used for metrics?

MySQL metrics are collected with different resolutions (5 seconds, 10 seconds,
and 60 seconds by default). Linux and MongoDB metrics are collected with 1
second resolution.

In case of bad network connectivity between {{ pmm_server }} and {{ pmm_client }} or
between {{ pmm_client }} and the database server it is monitoring, scraping every
second may not be possible when latency is higher than 1 second.

You can change the minimum resolution for metrics by the following way:


1. Select the {{ pmm_settings }} dashboard in the main menu.


2. In the *Settings* section, choose proper metrics resolution with the slider.
The tooltip of the slider will show you actual resolution values.


3. Click the *Apply changes* button.

**NOTE**: Consider increasing minimum resolution
when {{ pmm_server }} and {{ pmm_client }} are on different networks,
or when Adding an Amazon RDS MySQL, Aurora MySQL, or Remote Instance.

## How to set up Alerting in PMM?

You can make PMM Server trigger alerts when your monitored service reaches some thresholds in two ways:


* using [Grafana Alerting feature](https://grafana.com/docs/grafana/latest/alerting/rules/),


* using external [Alertmanager](https://github.com/prometheus/alertmanager) (a
high-performance solution developed by the Prometheus project to handle alerts sent
by Prometheus).

Both options can be considered advanced features and require knowledge of
third-party documentation.

Either with Grafana Alerting or with Alertmanager you need to configure some
alerting rule to define conditions under which the alert should be triggered,
and the channel used to send the alert (e.g. email).

Grafana Alerts are already integrated into PMM Server and may be simpler to get set up,
while Alertmanager allows the creation of more sophisticated alerting rules and
can be easier to manage installations with a large number of hosts; this
additional flexibility comes at the expense of simplicity and requires advanced
knowledge of Alertmanager rules. Currently Percona cannot offer support for
creating custom rules so you should already have a working Alertmanager instance
prior to using this feature, however we are working hard to bring an integrated
Alertmanager solution to make rule generation easy!

### [How to set up Alerting with Grafana](https://www.percona.com/doc/percona-monitoring-and-management/2.x/faq.html#how-to-setup-alerting-with-Grafana)

Alerting in Grafana allows attaching rules to your dashboard panels. Details
about Grafana Alerting Engine and Rules can be found in the [official documentation](https://grafana.com/docs/grafana/latest/alerting/rules/).
Setting it up and running within PMM Server is covered [by the following blog post](https://www.percona.com/blog/2017/02/02/pmm-alerting-with-grafana-working-with-templated-dashboards/).

### [How to integrate Alertmanager with PMM](https://www.percona.com/doc/percona-monitoring-and-management/2.x/faq.html#how-to-integrate-alertmanager-with-pmm)

PMM allows you to integrate Prometheus with an external Alertmanager.
Configuration is done on the [PMM Settings dashboard](https://www.percona.com/doc/percona-monitoring-and-management/2.x/manage/server-admin-gui.html).  The Alertmanager section in it allows specifying the URL of the Alertmanager
to serve your PMM alerts, as well as your [alerting rules in the YAML configuration format](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/).

More details on the Alertmanager and its alerting rules can be found in the
[official Alertmanager documentation](https://prometheus.io/docs/alerting/alertmanager/), which also provides plain examples of the [alerting rules](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/).

## How to use a custom Prometheus configuration file inside of a PMM Server?

Normally PMM Server fully manages [Prometheus configuration file](https://prometheus.io/docs/prometheus/latest/configuration/configuration/). Still, some users may want to be able to change generated configuration to add additional scrape jobs, configure remote storage, etc.

Starting from the version 2.4.0, when pmm-managed starts the Prometheus file
generation process, it tries to load the `/srv/prometheus/prometheus.base.yml`
file first, to use it as a base for the `prometheus.yml` if present and can be
parsed.

**NOTE**: The `prometheus.yml` file can be regenerated by restarting the PMM
Server container, or by the `SetSettings` [API call](https://www.percona.com/doc/percona-monitoring-and-management/2.x/manage/server-pmm-api.html) with an empty body.

You can find more details about using a custom Prometheus configuration file with
PMM [in a separate blog post](https://www.percona.com/blog/2020/03/23/extending-pmm-prometheus-configuration/).
