# Running {{ pmm_server }} via {{ docker }}

{{ docker }} images of {{ pmm_server }} are stored at the [percona/pmm-server](https://hub.docker.com/r/percona/pmm-server/tags/) public
repository. The host must be able to run {{ docker }} 1.12.6 or later, and have
network access.

{{ pmm }} needs roughly 1GB of storage for each monitored database node with data
retention set to one week. Minimum memory is 2 GB for one monitored database
node, but it is not linear when you add more nodes.  For example, data from 20
nodes should be easily handled with 16 GB.

Make sure that the firewall and routing rules of the host do not constrain the
{{ docker }} container. For more information, see How to troubleshoot communication issues between PMM Client and PMM Server?.

For more information about using {{ docker }}, see the [Docker Docs](https://docs.docker.com).


* Setting Up a {{ docker }} Container for {{ pmm_server }}


* Updating {{ pmm_server }} Using {{ docker }}


* Backing Up {{ pmm }} Data from the {{ docker }} Container


* Restoring the Backed Up Information to the PMM Data Container
