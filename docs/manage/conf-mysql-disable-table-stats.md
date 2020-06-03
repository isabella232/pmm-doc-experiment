# Improving PMM Performance with Table Statistics Options

If a {{ mysql }} instance has a lot of schemas or tables,
there are two options to help improve the performance of {{ pmm }}
when adding instances with {{ pmm_admin_add }}:
{{ opt_dis_tablestats }} and {{ opt_dis_tablestats_limit }}.

## Disable per-table statistics for an instance

When adding an instance with {{ pmm_admin_add }},
the {{ opt_dis_tablestats }} option
disables table statistics collection
when there are more than the default number (1000) of tables in the instance.

### USAGE

```
sudo pmm-admin add mysql --disable-tablestats
```

## Change the number of tables beyond which per-table statistics is disabled

When adding an instance with {{ pmm_admin_add }},
the {{ opt_dis_tablestats_limit }} option
changes the number of tables (from the default of 1000)
beyond which per-table statistics collection is disabled.

### USAGE

```
sudo pmm-admin add mysql --disable-tablestats-limit=<LIMIT>
```

### EXAMPLE

Add a {{ mysql }} instance,
disabling per-table statistics collection
when the number of tables in the instance reaches 2000.

```
sudo pmm-admin add mysql --disable-tablestats-limit=2000
```
