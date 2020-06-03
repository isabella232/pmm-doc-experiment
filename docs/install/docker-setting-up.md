# Setting Up a Docker Container for PMM Server

A {{ docker }} image is a collection of preinstalled software which enables running
a selected version of {{ pmm_server }} on your computer. A {{ docker }} image is not
run directly. You use it to create a {{ docker }} container for your {{ pmm_server }}.
When launched, the {{ docker }} container gives access to the whole functionality
of {{ pmm }}.

The setup begins with pulling the required {{ docker }} image. Then, you proceed by
creating a special container for persistent {{ pmm }} data. The last step is
creating and launching the {{ pmm_server }} container.

## [Pulling the PMM Server Docker Image](docker-setting-up.md#pmm-server-docker-image-pulling)

To pull the latest version from Docker Hub:

```
$ docker pull percona/pmm-server:2
```

This step is not required if you are running {{ pmm_server }} for the first time.
However, it ensures that if there is an older version of the image tagged with
`2.6.0` available locally, it will be replaced by the actual latest
version.

## [Creating the pmm-data Container](docker-setting-up.md#data-container)

To create a container for persistent {{ pmm }} data, run the following command:

```
$ docker create \
   -v /srv \
   --name pmm-data \
   percona/pmm-server:2 /bin/true
```

**NOTE**: This container does not run, it simply exists to make sure you retain
all {{ pmm }} data when you upgrade to a newer {{ pmm_server }} image.  Do not remove
or re-create this container, unless you intend to wipe out all {{ pmm }} data and
start over.

The previous command does the following:


* The {{ docker_create }} command instructs the {{ docker }} daemon
to create a container from an image.


* The {{ opt_v }} options initialize data volumes for the container.


* The {{ opt_name }} option assigns a custom name for the container
that you can use to reference the container within a {{ docker }} network.
In this case: `pmm-data`.


* `percona/pmm-server:2` is the name and version tag of the image
to derive the container from.


* `/bin/true` is the command that the container runs.

## [Creating and Launching the PMM Server Container](docker-setting-up.md#server-container)

To create and launch {{ pmm_server }} in one command, use {{ docker_run }}:

```
$ docker run -d \
   -p 80:80 \
   -p 443:443 \
   --volumes-from pmm-data \
   --name pmm-server \
   --restart always \
   percona/pmm-server:2
```

This command does the following:


* The {{ docker_run }} command runs a new container based on the
{{ opt_pmm_server_latest }} image.


* The {{ opt_p }} option maps the host port to the server port inside the docker
container for accessing the {{ pmm_server }} web UI in the format of
`-p <hostPort>:<containerPort>`. For example, if port **80** is not
available on your host, you can map the landing page to port 8080 using
`-p 8080:80`, the same for port **443**: `-p 8443:443`.


* The `--volumes-from` option mounts volumes from the `pmm-data` container
created previously (see Creating the pmm-data Container).


* The {{ opt_name }} option assigns a custom name to the container
that you can use to reference the container within the {{ docker }} network.
In this case: `pmm-server`.


* The {{ opt_restart }} option defines the container’s restart policy.
Setting it to `always` ensures that the Docker daemon
will start the container on startup
and restart it if the container exits.


* {{ opt_pmm_server_latest }} is the name and version tag of the image
to derive the container from.

## [Installing and using specific PMM Server version](docker-setting-up.md#pmm-docker-specific-version)

To install a specific {{ pmm_server }} version instead of the latest one, just put
desired version number after the colon. Also in this scenario it may be useful
to [prevent updating PMM Server via the web interface](https://www.percona.com/doc/percona-monitoring-and-management/glossary.option.html) with the `DISABLE_UPDATES` docker option.

Following docker tags are currently available to represent PMM Server versions:


* `:latest` currently means the latest release of the PMM 1.X


* `:2` is the latest released version of PMM 2


* `:2.X` can be used to refer any minor released version, excluding patch
releases


* `:2.X.Y` tag means specific patch release of PMM

For example, installing the latest 2.x version with disabled update button in
the web interface would look as follows:

```
$ docker create \
   -v /srv \
   --name pmm-data \
   percona/pmm-server:2 /bin/true

$ docker run -d \
   -p 80:80 \
   -p 443:443 \
   --volumes-from pmm-data \
   --name pmm-server \
   -e DISABLE_UPDATES=true \
   --restart always \
   percona/pmm-server:2
```
