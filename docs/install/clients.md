# [Installing Clients](clients.md#installing)

{{ pmm_client }} is a package of agents and exporters installed on a database host
that you want to monitor. Before installing the {{ pmm_client }} package on each
database host that you intend to monitor, make sure that your {{ pmm_server }} host
is accessible.

For example, you can run the {{ ping }} command passing the IP address of the
computer that {{ pmm_server }} is running on. For example:

```
$ ping 192.168.100.1
```

You will need to have root access on the database host where you will be
installing {{ pmm_client }} (either logged in as a user with root privileges or be
able to run commands with {{ sudo }}).

### Supported platforms

{{ pmm_client }} should run on any modern {{ linux }} 64-bit distribution, however
{{ percona }} provides {{ pmm_client }} packages for automatic installation from
software repositories only on the most popular {{ linux }} distributions:


* DEB packages for Debian based distributions such as Ubuntu


* RPM packages for Red Hat based distributions such as CentOS

It is recommended that you install your {{ abbr_pmm }} client by using the
software repository for your system. If this option does not work for you,
{{ percona }} provides downloadable {{ pmm_client }} packages
from the [Download Percona Monitoring and Management](https://www.percona.com/downloads/pmm-client) page.

In addition to DEB and RPM packages, this site also offers:


* Generic tarballs that you can extract and run the included `install` script.


* Source code tarball to build your {{ abbr_pmm }} client from source.

!!! warning
    You should not install agents on database servers that have the same host name, because host names are used by {{ pmm_server }} to identify collected data.

### Storage requirements

Minimum **100** MB of storage is required for installing the {{ pmm_client }}
package. With a good constant connection to {{ pmm_server }}, additional storage is
not required. However, the client needs to store any collected data that it is
not able to send over immediately, so additional storage may be required if
connection is unstable or throughput is too low.
