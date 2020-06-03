# Updating PMM Server Using Docker

To check the version of {{ pmm_server }}, run {{ docker_ps }} on the host.

{{ tip_run_all_root }}

```
$ docker ps
CONTAINER ID  IMAGE                     COMMAND                CREATED       STATUS             PORTS                                      NAMES
4bdcc8463e64  percona/pmm-server:2.2.0  "/opt/entrypoint.sh"   2 weeks ago   Up About an hour   0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   pmm-server
```

The version number is visible in the {{ gui_image }} column. For a {{ docker }}
container created from the image tagged `2`, the {{ gui_image }} column
contains `2` and not the specific version number of {{ pmm_server }}.

The information about the currently installed version of {{ pmm_server }} is
available from the {{ srv_update_main_yml }} file. You may extract the version
number by using the {{ docker_exec }} command:

```
$ docker exec -it pmm-server head -1 /srv/update/main.yml
# v1.5.3
```

To check if there exists a newer version of {{ pmm_server }},
visit [percona/pmm-server](https://hub.docker.com/r/percona/pmm-server/tags/).

## [Creating a backup version of the current pmm-server Docker container](docker-upgrading.md#container-renaming)

You need to create a backup version of the current {{ opt_pmm_server }} container if
the update procedure does not complete successfully or if you decide not to
upgrade your {{ pmm_server }} after trying the new version.

The {{ docker_stop }} command stops the currently running {{ opt_pmm_server }} container:

```
$ docker stop pmm-server
```

The following command simply renames the current {{ opt_pmm_server }} container to
avoid name conflicts during the update procedure:

```
$ docker rename pmm-server pmm-server-backup
```

## [Pulling a new Docker Image](docker-upgrading.md#image-pulling)

{{ docker }} images for all versions of {{ pmm }} are available from
[percona/pmm-server](https://hub.docker.com/r/percona/pmm-server/tags/)
{{ docker }} repository.

When pulling a newer {{ docker }} image, you may either use a specific version
number or the `2` image which always matches the highest version
number.

This example shows how to pull a specific version:

This example shows how to pull the latest PMM 2 version:

```
$ docker pull percona/pmm-server:2
```

## [Creating a new Docker container based on the new image](docker-upgrading.md#container-creating)

After you have pulled a new version of {{ pmm }} from the {{ docker }} repository, you can
use {{ docker_run }} to create a {{ opt_pmm_server }} container using the new image.

```
$ docker run -d \
   -p 80:80 \
   -p 443:443 \
   --volumes-from pmm-data \
   --name pmm-server \
   --restart always \
   percona/pmm-server:2
```

The {{ docker_run }} command refers to the pulled image as the last parameter. If
you used a specific version number when running {{ docker_pull }} (see
Pulling the PMM Server Docker Image) replace `2` accordingly.

Note that this command also refers to {{ opt_pmm_data }} as the value of
{{ opt_volumes_from }} option. This way, your new version will continue to use the
existing data.

!!! warning 
    Do not remove the {{ opt_pmm_data }} container when updating, if you want to keep all collected data.

Check if the new container is running using {{ docker_ps }}.

```
$ docker ps
CONTAINER ID   IMAGE                      COMMAND                CREATED         STATUS         PORTS                               NAMES
480696cd4187   percona/pmm-server:1.5.0   "/opt/entrypoint.sh"   4 minutes ago   Up 4 minutes   192.168.100.1:80->80/tcp, 443/tcp   pmm-server
```

Then, make sure that the {{ pmm }} version has been updated (see PMM
Version) by checking the {{ pmm_server }} web interface.

## [Removing the backup container](docker-upgrading.md#backup-container-removing)

After you have tried the features of the new version, you may decide to
continupe using it. The backup container that you have stored
(Creating a backup version of the current pmm-server Docker container) is no longer needed in this
case.

To remove this backup container, you need the {{ docker_rm }} command:

```
$ docker rm pmm-server-backup
```

As the parameter to {{ docker_rm }}, supply the tag name of your backup container.

### Restoring the previous version

If, for whatever reason, you decide to keep using the old version, you just need
to stop and remove the new {{ opt_pmm_server }} container.

```
$ docker stop pmm-server && docker rm pmm-server
```

Now, rename the {{ opt_pmm_server_backup }} to {{ opt_pmm_server }}
(see Creating a backup version of the current pmm-server Docker container) and start it.

```
$ docker start pmm-server
```

!!! warning
    Do not use the {{ docker_run }} command to start the container. The {{ docker_run }} command creates and then runs a new container.

To start a new container use the {{ docker_start }} command.

<!-- References -->
