# Required AWS settings

It is possible to use {{ pmm }} for monitoring {{ amazon_rds }} (just like any remote {{ mysql }} instance). In this case, the {{ pmm_client }} is not installed on the host where the database server is deployed. By using the {{ pmm }} web interface, you connect to the {{ amazon_rds }} DB instance. You only need to provide the {{ iam }} user access key (or assign an IAM role) and {{ pmm }} discovers the {{ amazon_rds }} DB instances available for monitoring.

First of all, ensure that there is the minimal latency between {{ pmm_server }} and the
{{ amazon_rds }} instance.

Network connectivity can become an issue for {{ prometheus }} to scrape
metrics with 1 second resolution.  We strongly suggest that you run
{{ pmm_server }} on {{ abbr_aws }} in the same availability zone as
{{ amazon_rds }} instances.

It is crucial that *enhanced monitoring* be enabled for the {{ amazon_rds }} DB
instances you intend to monitor.

## [Creating an IAM user with permission to access Amazon RDS DB instances](amazon-rds-settings.md#pmm-amazon-rds-permission-access-db-instance-iam-user-creating)

It is recommended that you use an {{ iam }} user account to access {{ amazon_rds }}
DB instances instead of using your {{ aws }} account. This measure improves security
as the permissions of an {{ iam }} user account can be limited so that this account
only grants access to your {{ amazon_rds }} DB instances. On the other
hand, you use your {{ aws }} account to access all {{ aws }} services.

The procedure for creating {{ iam }} user accounts is well described in the
{{ amazon_rds }} documentation. This section only goes through the essential steps
and points out the steps required for using {{ amazon_rds }} with {{ percona_monitoring_management }}.

The first step is to define a policy which will hold all the necessary
permissions. Then, you need to associate this policy with the IAM user or
group. In this section, we will create a new user for this purpose.

## [Creating a policy](amazon-rds-settings.md#pmm-amazon-rds-iam-user-policy)

A policy defines how {{ aws }} services can be accessed. Once defined it can be
associated with an existing user or group.

To define a new policy use the {{ iam }} page at {{ aws }}.


1. Select the {{ gui_policies }} option on the navigation panel and click the
{{ gui_create_policy }} button.


2. On the {{ gui_create_policy }} page, select the {{ json }} tab and replace the
existing contents with the following {{ json }} document.

```
{ "Version": "2012-10-17",
  "Statement": [{ "Sid": "Stmt1508404837000",
                  "Effect": "Allow",
                  "Action": [ "rds:DescribeDBInstances",
                              "cloudwatch:GetMetricStatistics",
                              "cloudwatch:ListMetrics"],
                              "Resource": ["*"] },
                 { "Sid": "Stmt1508410723001",
                   "Effect": "Allow",
                   "Action": [ "logs:DescribeLogStreams",
                               "logs:GetLogEvents",
                               "logs:FilterLogEvents" ],
                               "Resource": [ "arn:aws:logs:*:*:log-group:RDSOSMetrics:*" ]}
               ]
}
```


3. Click {{ gui_review_policy }} and set a name to your policy, such as
*AmazonRDSforPMMPolicy*. Then, click the {{ gui_create_policy }} button.

## [Creating an IAM user](amazon-rds-settings.md#pmm-amazon-rds-iam-user-creating)

Policies are attached to existing {{ iam }} users or groups. To create a new {{ iam }}
user, select {{ gui_users }} on the {{ identity_access_management }} page at {{ aws }}. Then click
{{ gui_add_user }} and complete the following steps:


1. On the {{ gui_add_user }} page, set the user name and select the
{{ gui_programmatic_access }} option under
{{ gui_select_aws_access_type }}. Set a custom password and then proceed to
permissions by clicking the {{ gui_permissions }} button.


2. On the {{ gui_set_permissions }} page, add the new user to one or more groups if
necessary. Then, click {{ gui_review }}.


3. On the {{ gui_add_user }} page, click {{ gui_create_user }}.

## [Creating an access key for an IAM user](amazon-rds-settings.md#pmm-amazon-rds-iam-user-access-key-creating)

In order to be able to discover an {{ amazon_rds }} DB instance in {{ pmm }}, you either
need to use the access key and secret access key of an existing {{ iam }} user or an
{{ iam }} role. To create an access key for use with {{ pmm }}, open the {{ iam }} console
and click {{ gui_users }} on the navigation pane. Then, select your {{ iam }} user.

To create the access key, open the {{ gui_security_credentials }} tab and click the
{{ gui_create_access_key }} button. The system automatically generates a new access
key ID and a secret access key that you can provide on the {{ pmm_add_instance }}
dashboard to have your {{ amazon_rds }} DB instances discovered.

In case, the {{ pmm_server }} and {{ amazon_rds }} DB instance were created by using the
same {{ aws }} account, you do not need create the access key ID and secret access
key manually. {{ pmm }} retrieves this information automatically and attempts to
discover your {{ amazon_rds }} DB instances.

## [Attaching a policy to an IAM user](amazon-rds-settings.md#pmm-amazon-rds-iam-user-policy-attaching)

The last step before you are ready to create an {{ amazon_rds }} DB instance is to
attach the policy with the required permissions to the {{ iam }} user.

First, make sure that the {{ identity_access_management }} page is open and open
{{ gui_users }}. Then, locate and open the {{ iam }} user that you plan to use with
{{ amazon_rds }} DB instances. Complete the following steps, to apply the policy:


1. On the {{ gui_permissions }} tab, click the {{ gui_add_permissions }} button.


2. On the {{ gui_add_permissions }} page, click {{ gui_attach_existing_policies_directly }}.


3. Using the {{ gui_filter }}, locate the policy with the required permissions (such as *AmazonRDSforPMMPolicy*).


4. Select a checkbox next to the name of the policy and click {{ gui_review }}.


5. The selected policy appears on the {{ gui_permissions_summary }} page. Click {{ gui_add_permissions }}.

The *AmazonRDSforPMMPolicy* is now added to your {{ iam }} user.

## [Setting up the Amazon RDS DB Instance](amazon-rds-settings.md#pmm-amazon-rds-db-instance-setting-up)

{{ query_analytics }} requires Configuring Performance Schema as the query source, because the slow
query log is stored on the {{ abbr_aws }} side, and {{ qan }} agent is not able to
read it.  Enable the `performance_schema` option under `Parameter Groups`
in {{ amazon_rds }}.

**WARNING**: Enabling Performance Schema on T2 instances is not recommended
because it can easily run the T2 instance out of memory.

When adding a monitoring instance for {{ amazon_rds }}, specify a unique name to
distinguish it from the local {{ mysql }} instance.  If you do not specify a name,
it will use the client’s host name.

Create the `pmm` user with the following privileges on the {{ amazon_rds }}
instance that you want to monitor:

```
GRANT SELECT, PROCESS, REPLICATION CLIENT ON *.* TO 'pmm'@'%' IDENTIFIED BY 'pass' WITH MAX_USER_CONNECTIONS 10;
GRANT SELECT, UPDATE, DELETE, DROP ON performance_schema.* TO 'pmm'@'%';
```

If you have {{ amazon_rds }} with a {{ mysql }} version prior to 5.5, REPLICATION
CLIENT privilege is not available there and has to be excluded from the above
statement.

**NOTE**: General system metrics are monitored by using the {{ rds_exporter }} {{ prometheus }}
exporter which replaces {{ node_exporter }}. {{ rds_exporter }} gives acces to
{{ amazon_cloudwatch }} metrics.

{{ node_exporter }}, used in versions of {{ pmm }} prior to 1.8.0, was not able to
monitor general system metrics remotely.
