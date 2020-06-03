# MongoDB requirements

## Configuring MongoDB for Monitoring in {{ qan_name }}

In {{ abbr_qan }}, you can monitor {{ mongodb }} metrics and {{ mongodb }} queries. Run the
{{ pmm_admin_add }} command to use these monitoring services
(for more information, see Adding MongoDB Service Monitoring).

### Supported versions of {{ mongodb }}

{{ abbr_qan }} supports {{ mongodb }} version 3.2 or higher.

## Setting Up the Required Permissions

For {{ mongodb }} monitoring services to be able work in {{ abbr_qan }}, you need to
set up the {{ mongodb_exporter }} user. This user should be assigned the
{{ cluster_monitor }} and {{ readAnyDatabase }} roles for the {{ db_admin }} database.

The following is an example you can run in the {{ mongodb }} shell, to add the
{{ mongodb_exporter }} user and assign the appropriate roles:

## [Enabling Profiling](/conf-mongodb.md#pmm-qan-mongodb-configuring-profiling-enabling)

For [MongoDB](https://www.mongodb.com) to work correctly with {{ abbr_qan }}, you need to enable profiling
in your {{ mongod }} configuration. When started without profiling enabled, {{ qan }}
displays the following warning:

**NOTE**: **A warning message is displayed when profiling is not enabled**

It is required that profiling of the monitored {{ mongodb }} databases be enabled, however
profiling is not enabled by default because it may reduce the performance of your
{{ mongodb }} server.

### [Enabling Profiling on Command Line](/conf-mongodb.md#pmm-qan-mongodb-conf-profiling-command-line-enable)

You can enable profiling from command line when you start the **mongod**
server. This command is useful if you start **mongod** manually.

{{ tip_run_this_root }}

<!-- The following does not render on the live version -->
Note that you need to specify a path to an existing directory that stores
database files with the {{ opt_dbpath }}. When the {{ opt_profile }} option is set to
**2**, {{ mongod }} collects the profiling data for all operations. To decrease the
load, you may consider setting this option to **1** so that the profiling data
are only collected for slow operations.

The {{ opt_slowms }} option sets the minimum time for a slow operation. In the
given example, any operation which takes longer than **200** milliseconds is a
slow operation.

The {{ opt_rate_limit }} option, which is available if you use {{ psmdb }} instead
of {{ mongodb }}, refers to the number of queries that the {{ mongodb }} profiler
collects. The lower the rate limit, the less impact on the performance.
However, the accuracy of the collected information decreases as well.

### [Enabling Profiling in the Configuration File](/conf-mongodb.md#pmm-qan-mongodb-configuring-configuration-file-profiling-enabling)

If you run `mongod` as a service, you need to use the configuration file
which by default is {{ etc_mongod_conf }}.

In this file, you need to locate the *operationProfiling:* section and add the
following settings:

```
operationProfiling:
   slowOpThresholdMs: 200
   mode: slowOp
   rateLimit: 100
```

These settings affect `mongod` in the same way as the command line
options described in section
pmm.qan-mongodb.conf.profiling.command_line.enable. Note that the
configuration file is in the [YAML](http://yaml.org/spec/) format. In this format the indentation of
your lines is important as it defines levels of nesting.

Restart the *mongod* service to enable the settings.

{{ tip_run_this_root }}

<!-- The following does not show up on the live version -->
