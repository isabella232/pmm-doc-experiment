# Annotating important Application Events

## Adding annotations

Use the {{ pmm_admin_annotate }} command to set notifications about important
application events and display them on all dashboards. By using annotations, you
can conveniently analyze the impact of application events on your database.

### USAGE

{{ tip_run_this_root }}

### OPTIONS

The {{ pmm_admin_annotate }} supports the following options:

{{ opt_tags }}

> Specify one or more tags applicable to the annotation that you are
> creating. Enclose your tags in quotes and separate individual tags by a
> comma, such as “tag 1,tag 2”.

You can also use
global options that apply to any other command.

## Marking Important Events with Annotations [application-event-marking]

Some events in your application may impact your database. Annotations
visualize these events on each dashboard of {{ pmm_server }}.

To create a new annotation, run {{ pmm_admin_annotate }} command on
{{ pmm_client }} passing it text which explains what event the new
annotation should represent. Use the {{ opt_tags }} option to supply one
or more tags separated by a comma.

You may toggle displaying annotations on metric graphs by using the
{{ gui_pmm_annotations }} checkbox.
