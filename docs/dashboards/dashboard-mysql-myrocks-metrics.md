# {{ dbd_mysql_myrocks_metrics }} Dashboard

The [MyRocks](http://myrocks.io) storage engine developed by {{ facebook }} based on the {{ rocksdb }}
storage engine is applicable to systems which primarily interact with the
database by writing data to it rather than reading from it. {{ rocksdb }} also
features a good level of compression, higher than that of the {{ innodb }} storage
engine, which makes it especially valuable when optimizing the usage of hard
drives.

{{ pmm }} collects statistics on the {{ myrocks }} storage engine for {{ mysql }} in the
{{ metrics_monitor }} information for this dashboard comes from the
{{ inf_schema }} tables.

### Metrics
