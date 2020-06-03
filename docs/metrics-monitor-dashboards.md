# Understanding Dashboards

The {{ metrics_monitor }} tool provides a {{ metrics_monitor_what_is }}. Time-based
graphs are separated into dashboards by themes: some are related to {{ mysql }} or
{{ mongodb }}, others provide general system metrics.

## [Opening a Dashboard](metrics-monitor-dashboards.md#pmm-metrics-monitor-dashboard-opening)

The default {{ pmm }} installation provides more than thirty dashboards. To make it
easier to reach a specific dashboard, the system offers two tools. The
{{ gui_dashboard_dropdown }} is a button in the header of any {{ pmm }} page. It lists
all dashboards, organized into folders. Right sub-panel allows to rearrange
things, creating new folders and dragging dashboards into them. Also a text box
on the top allows to search the required dashboard by typing.

## [Viewing More Information about a Graph](metrics-monitor-dashboards.md#pmm-metrics-monitor-graph-description)

Each graph has a descriptions to display more information about the monitored
data without cluttering the interface.

These are on-demand descriptions in the tooltip format that you can find by
hovering the mouse pointer over the {{ gui_more_information }} icon at the top left
corner of a graph. When you move the mouse pointer away from the {{ gui_more_inf }}
button the description disappears.
