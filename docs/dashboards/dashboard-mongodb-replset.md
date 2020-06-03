# {{ mongodb }} ReplSet

This dashboard provides information about replica sets and their members.

## [Replication Operations](dashboard-mongodb-replset.md#replication-operations)

This metric provides an overview of database replication operations by type and
makes it possible to analyze the load on the replica in more granular
manner. These values only appear when the current host has replication enabled.

## [ReplSet State](dashboard-mongodb-replset.md#replset-state)

This metric shows the role of the selected member instance (PRIMARY or SECONDARY).

{{ view_all_metrics }} {{ mongodb }} ReplSet

## [ReplSet Members](dashboard-mongodb-replset.md#replset-members)

This metric the number of members in the replica set.

{{ view_all_metrics }} {{ mongodb }} ReplSet

## ReplSet Last Election

This metric how long ago the last election occurred.

{{ view_all_metrics }} {{ mongodb }} ReplSet

## [ReplSet Lag](dashboard-mongodb-replset.md#replset-lag)

This metric shows the current replication lag for the selected member.

{{ view_all_metrics }} {{ mongodb }} ReplSet

## [Storage Engine](dashboard-mongodb-replset.md#storage-engine)

This metric shows the storage engine used on the instance

{{ view_all_metrics }} {{ mongodb }} ReplSet

## [Oplog Insert Time](dashboard-mongodb-replset.md#oplog-insert-time)

This metric shows how long it takes to write to the oplog. Without it the write
will not be successful.

This is more useful in mixed replica sets (where instances run different storage
engines).

{{ view_all_metrics }} {{ mongodb }} ReplSet

## [Oplog Recovery Window](dashboard-mongodb-replset.md#oplog-recovery-window)

This metric shows the time range in the oplog and the oldest backed up
operation.

For example, if you take backups every 24 hours, each one should contain at
least 36 hours of backed up operations, giving you 12 hours of restore window.

{{ view_all_metrics }} {{ mongodb }} ReplSet

## [Replication Lag](dashboard-mongodb-replset.md#replication-lag)

This metric shows the delay between an operation occurring on the primary and
that same operation getting applied on the selected member

{{ view_all_metrics }} {{ mongodb }} ReplSet

## [Elections](dashboard-mongodb-replset.md#elections)

Elections happen when a primary becomes unavailable. Look at this graph over
longer periods (weeks or months) to determine patterns and correlate elections
with other events.

{{ view_all_metrics }} {{ mongodb }} ReplSet

## [Member State Uptime](dashboard-mongodb-replset.md#member-state-uptime)

This metric shows how long various members were in PRIMARY and SECONDARY roles.

{{ view_all_metrics }} {{ mongodb }} ReplSet

## [Max Heartbeat Time](dashboard-mongodb-replset.md#max-heartbeat-time)

This metric shows the heartbeat return times sent by the current member to other
members in the replica set.

Long heartbeat times can indicate network issues or that the server is too busy.

{{ view_all_metrics }} {{ mongodb }} ReplSet

## [Max Member Ping Time](dashboard-mongodb-replset.md#max-member-ping-time)

This metric can show a correlation with the replication lag value.

{{ view_all_metrics }} {{ mongodb }} ReplSet
