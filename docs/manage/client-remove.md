# Removing monitoring services with pmm-admin remove

Use the {{ pmm_admin_rm }} command to remove monitoring services.

### USAGE

{{ tip_run_this_root }}

```
pmm-admin remove [OPTIONS] [SERVICE-TYPE] [SERVICE-NAME]
```

When you remove a service,
collected data remains in {{ metrics_monitor }} on {{ pmm_server }}.

### SERVICES

Service type can be mysql, mongodb, postgresql or proxysql, and service
name is a monitoring service alias. To see which services are enabled,
run **pmm-admin list**.

### EXAMPLES


* Removing {{ mysql }} service named “mysql-sl”:

```
# pmm-admin remove mysql mysql-sl
Service removed.
```


* To remove *MongoDB* service named “mongo”:

```
# pmm-admin remove mongodb mongo
Service removed.
```


* To remove *PostgreSQL* service named “postgres”:

```
# pmm-admin remove postgresql postgres
Service removed.
```


* To remove *ProxySQL* service named “ubuntu-proxysql”:

```
# pmm-admin remove proxysql ubuntu-proxysql
Service removed.
```

For more information, run {{ pmm_admin_rm }} –help.
