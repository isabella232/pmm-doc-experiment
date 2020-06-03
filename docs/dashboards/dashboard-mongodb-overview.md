# {{ mongodb }} Overview

This dashboard provides basic information about {{ mongodb }} instances.

## [Command Operations](dashboard-mongodb-overview.md#command-operations)

Shows how many times a command is executed per second on average during the
selected interval.

Look for peaks and drops and correlate them with other graphs.

{{ view_all_metrics }} {{ mongodb }} Overview

## [Connections](dashboard-mongodb-overview.md#connections)

Keep in mind the hard limit on the maximum number of connections set by your
distribution.

Anything over 5,000 should be a concern, because the application may not close
connections correctly.

{{ view_all_metrics }} {{ mongodb }} Overview

## [Cursors](dashboard-mongodb-overview.md#cursors)

Helps identify why connections are increasing.  Shows active cursors compared to
cursors being automatically killed after 10 minutes due to an application not
closing the connection.

{{ view_all_metrics }} {{ mongodb }} Overview

## [Document Operations](dashboard-mongodb-overview.md#document-operations)

When used in combination with **Command Operations**, this graph can help
identify *write aplification*.  For example, when one `insert` or `update`
command actually inserts or updates hundreds, thousands, or even millions of
documents.

{{ view_all_metrics }} {{ mongodb }} Overview

## [Queued Operations](dashboard-mongodb-overview.md#queued-operations)

Any number of queued operations for long periods of time is an indication of
possible issues.  Find the cause and fix it before requests get stuck in the
queue.

{{ view_all_metrics }} {{ mongodb }} Overview

## [getLastError Write Time, getLastError Write Operations](dashboard-mongodb-overview.md#getlasterror-write-time.operations)

This is useful for write-heavy workloads to understand how long it takes to
verify writes and how many concurrent writes are occurring.

{{ view_all_metrics }} {{ mongodb }} Overview

## [Asserts](dashboard-mongodb-overview.md#asserts)

Asserts are not important by themselves, but you can correlate spikes with other
graphs.

{{ view_all_metrics }} {{ mongodb }} Overview

## [Memory Faults](dashboard-mongodb-overview.md#memory-faults)

Memory faults indicate that requests are processed from disk either because an
index is missing or there is not enough memory for the data set.  Consider
increasing memory or sharding out.

{{ view_all_metrics }} {{ mongodb }} Overview
