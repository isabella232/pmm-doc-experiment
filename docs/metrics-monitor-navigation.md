# Navigating across Dashboards

Beside the {{ gui_dashboard_dropdown }} button you can also Navigate across
Dashboards with the navigation menu which groups dashboards by
application. Click the required group and then select the dashboard
that matches your choice.

| Group               | Dashboards for monitoring
|---------------------|----------------------------------------------------
| {{ qan_name }}      | {{ qan }} component (see Introduction)
| OS                  | The operating system status
| {{ mysql }}         | {{ mysql }} and {{ amazon_aurora }}
| {{ mongodb }}       | State of {{ mongodb }} hosts
| HA                  | High availability
| Cloud               | {{ amazon_rds }} and {{ amazon_aurora }}
| Insight             | Summary, cross-server and {{ prometheus }}
| {{ pmm }}           | Server settings

## Zooming in on a single metric [pmm.metrics-monitor.metric.zooming-in]

On dashboards with multiple metrics, it is hard to see how the value of a single
metric changes over time. Use the context menu to zoom in on the selected metric
so that it temporarily occupies the whole dashboard space.

Click the title of the metric that you are interested in and select the
{{ gui_view }} option from the context menu that opens.

The selected metric opens to occupy the whole dashboard space. You may now set
another time range using the time and date range selector at the top of the
{{ metrics_monitor }} page and analyze the metric data further.

To return to the dashboard, click the {{ gui_back_to_dashboard }} button next to the time range selector.

Navigation menu allows you to navigate between dashboards while maintaining the
same host under observation and/or the same selected time range, so that for
example you can start on *MySQL Overview* looking at host serverA, switch to
MySQL InnoDB Advanced dashboard and continue looking at serverA, thus saving you
a few clicks in the interface.
