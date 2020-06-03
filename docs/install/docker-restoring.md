# Restoring the Backed Up Information to the PMM Data Container

If you have a backup copy of your {{ opt_pmm_data }} container, you can restore it
into a {{ docker }} container. Start with renaming the existing {{ pmm }} containers to
prevent data loss, create a new {{ opt_pmm_data }} container, and finally copy the
backed up information into the {{ opt_pmm_data }} container.

{{ tip_run_all_root }}


1. Stop the running {{ opt_pmm_server }} container.

```
$ docker stop pmm-server
```


2. Rename the {{ opt_pmm_server }} container to {{ opt_pmm_server_backup }}.

```
$ docker rename pmm-server pmm-server-backup
```


3. Rename the {{ opt_pmm_data }} to {{ opt_pmm_data_backup }}

```
$ docker rename pmm-data pmm-data-backup
```


4. Create a new {{ opt_pmm_data }} container

```
$ docker create \
   -v /srv \
   --name pmm-data \
   percona/pmm-server:2 /bin/true
```

Assuming that you have a backup copy of your {{ opt_pmm_data }}, created according
to the procedure described in the:ref:pmm.server.docker-backing-up section,
restore your data as follows:


1. Change the working directory to the directory that contains your
{{ opt_pmm_data }} backup files.

```
$ cd ~/pmm-data-backup
```

**NOTE**: This example assumes that the backup directory is found in your
home directory.


2. Copy data from your backup directory to the {{ opt_pmm_data }} container.

```
$ docker cp opt/prometheus/data pmm-data:/opt/prometheus/
$ docker cp opt/consul-data pmm-data:/opt/
$ docker cp var/lib/mysql pmm-data:/var/lib/
$ docker cp var/lib/grafana pmm-data:/var/lib/
```


3. Apply correct ownership to {{ opt_pmm_data }} files:

```
$ docker run --rm --volumes-from pmm-data -it percona/pmm-server:2 chown -R pmm:pmm /opt/prometheus/data /opt/consul-data
$ docker run --rm --volumes-from pmm-data -it percona/pmm-server:2 chown -R grafana:grafana /var/lib/grafana
$ docker run --rm --volumes-from pmm-data -it percona/pmm-server:2 chown -R mysql:mysql /var/lib/mysql
```


4. Run (create and launch) a new {{ opt_pmm_server }} container:

```
$ docker run -d \
   -p 80:80 \
   -p 443:443 \
   --volumes-from pmm-data \
   --name pmm-server \
   --restart always \
   percona/pmm-server:2
```

To make sure that the new server is available run the {{ pmm_admin_check_network }}
command from the computer where {{ pmm_client }} is installed. {{ tip_run_this_root }}.

```
$ pmm-admin check-network
```

<!-- References -->
