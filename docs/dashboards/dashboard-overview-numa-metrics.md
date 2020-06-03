# {{ dbd_overview_numa_metrics }} Dashboard

For each node, this dashboard shows metrics related to Non-uniform memory
access (NUMA).

## [Memory Usage](dashboard-overview-numa-metrics.md#memory-usage)

Remotes over time the total, used, and free memory.

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard

## [Free Memory Percent](dashboard-overview-numa-metrics.md#free-memory-percent)

Shows the free memory as the ratio to the total available memory.

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard

## [NUMA Memory Usage Types](dashboard-overview-numa-metrics.md#numa-memory-usage-types)

Dirty

    Memory waiting to be written back to disk

Bounce

    Memory used for block device bounce buffers

Mapped

    Files which have been mmaped, such as libraries

KernelStack The memory the kernel stack uses. This is not reclaimable.

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard

## [NUMA Allocation Hits](dashboard-overview-numa-metrics.md#numa-allocation-hits)

Memory successfully allocated on this node as intended.

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard

## [NUMA Allocation Missed](dashboard-overview-numa-metrics.md#numa-allocation-missed)

Memory missed is allocated on a node despite the process preferring some different node.

Memory foreign is intended for a node, but actually allocated on some different node.

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard

## [Anonymous Memory](dashboard-overview-numa-metrics.md#anonymous-memory)

Active

    Anonymous memory that has been used more recently and usually not swapped out.

Inactive

    Anonymous memory that has not been used recently and can be swapped out.

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard

## [NUMA File (PageCache)](dashboard-overview-numa-metrics.md#numa-file-page-cache)

Active(file) Pagecache memory that has been used more recently and usually not
reclaimed until needed.

Inactive(file) Pagecache memory that can be reclaimed without huge performance
impact.

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard

## [Shared Memory](dashboard-overview-numa-metrics.md#shared-memory)

Shmem Total used shared memory (shared between several processes, thus including
RAM disks, SYS-V-IPC and BSD like SHMEM)

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard

## [HugePages Statistics](dashboard-overview-numa-metrics.md#hugepages-statistics)

Total

    Number of hugepages being allocated by the kernel (Defined with vm.nr_hugepages).

Free

    The number of hugepages not being allocated by a process

Surp

    The number of hugepages in the pool above the value in vm.nr_hugepages. The
    maximum number of surplus hugepages is controlled by
    vm.nr_overcommit_hugepages.

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard

## [Local Processes](dashboard-overview-numa-metrics.md#local-processes)

Memory allocated on a node while a process was running on it.

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard

## [Remote Processes](dashboard-overview-numa-metrics.md#remote-processes)

Memory allocated on a node while a process was running on some other node.

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard

## [Slab Memory](dashboard-overview-numa-metrics.md#slab-memory)

Slab

    Allocation is a memory management mechanism intended for the efficient memory allocation of kernel objects.

SReclaimable

    The part of the Slab that might be reclaimed (such as caches).

SUnreclaim

    The part of the Slab that can’t be reclaimed under memory pressure

{{ view_all_metrics }} {{ dbd_overview_numa_metrics }} Dashboard
