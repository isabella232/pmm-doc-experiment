# Adding an Amazon RDS MySQL, Aurora MySQL, or Remote Instance

The {{ pmm_add_instance }} is now a preferred method of adding an {{ amazon_rds }}
database instance to {{ pmm }}. This method supports {{ amazon_rds }} database instances
that use {{ amazon_aurora }}, {{ mysql }}, or {{ mariadb }} engines, as well as any remote PostgreSQL, ProxySQL, MySQL and MongoDB instances.

Following steps are needed to add an {{ amazon_rds }} database instance to {{ pmm }}:


1. Open the {{ pmm }} web interface and select the {{ pmm_add_instance }} dashboard.

Choosing the {{ pmm }} *Add instance* menu entry


2. Select the {{ gui_add_rds_aurora_instance }} option in the dashboard.


3. Enter the access key ID and the secret access key of your {{ iam }} user.


4. Click the {{ gui_discover }} button for {{ pmm }} to retrieve the available {{ amazon_rds }}
instances.

For the instance that you would like to monitor, select the
{{ gui_start_monitoring }} button.


5. You will see a new page with the number of fields. The list is divided into
the following groups: *Main details*, *RDS database*, *Labels*, and
*Additional options*. Some already known data, such as already entered
*AWS access key*, are filled in automatically, and some fields are optional.

The *Main details* section allows to specify the DNS hostname of your instance,
service name to use within PMM, the port your service is listening on, the
database user name and password.

The *Labels* section allows specifying labels for the environment, the AWS
region and availability zone to be used, the Replication set and Cluster
names and also it allows to set the list of custom labels in a key:value
format.

The *Additional options* section contains specific flags which allow to tune
the RDS monitoring. They can allow you to skip connection check, to use TLS
for the database connection, not to validate the TLS certificate and the
hostname, as well as to disable basic and/or enhanced metrics collection for
the RDS instance to reduce costs.

We should allow users to disable basic and/or enhanced metrics when RDS instance is added.

> Also this section contains a database-specific flag, which would allow Query
> Analytics for the selected remote database:


> * when adding some remote MySQL, AWS RDS MySQL or Aurora MySQL instance, you
> will be able to choose using performance schema for the database monitoring


> * when adding a PostgreSQL instance, you will be able to activate using
> `pg_stat_statements` extension


> * when adding a MongoDB instance, you will be able to choose using
> QAN MongoDB profiler

# Finally press the {{ gui_add_service }} button to start monitoring your instance.
