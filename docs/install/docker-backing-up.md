# Backing Up {{ pmm }} Data from the {{ docker }} Container

When {{ pmm_server }} is run via {{ docker }}, its data are stored in the {{ opt_pmm_data }}
container. To avoid data loss, you can extract the data and store outside of the
container.

This example demonstrates how to back up {{ pmm }} data on the computer where the
{{ docker }} container is run and then how to restore them.

To back up the information from {{ opt_pmm_data }}, you need to create a local
directory with essential sub folders and then run {{ docker }} commands to copy
{{ pmm }} related files into it.


1. Create a backup directory and make it the current working directory. In this
example, we use *pmm-data-backup* as the directory name.

```
$ mkdir pmm-data-backup; cd pmm-data-backup
```


2. Create the essential sub directory:

```
$ mkdir srv
```

{{ tip_run_all_root }}


1. Stop the docker container:

```
$ docker stop pmm-server
```


2. Copy data from the {{ opt_pmm_data }} container:

```
$ docker cp pmm-data:/srv ./
```

Now, your {{ pmm }} data are backed up and you can start {{ pmm_server }} again:

```
$ docker start pmm-server
```
