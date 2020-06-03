# Filtering Queries

If you need to limit the list of available queries to only those that you are
interested in, use the filtering panel on the left, or use the filter by bar to
set filters using *key:value* syntax.

Following example shows how to filter just the queries that are executed on the
*Ubuntu* node. Note that Labels unavailable within the set of currently
applied filters are shown as gray/disabled on the filtering panel, and the
percentage values are dynamically recalculated to reflect the current selection.

By default Filter panel shows top 5 Labels in each section. The additional
“See all” link with the total number of Labels appears if their amount exceeds
five. Clicking this link toggles it into “Show top 5” and reveals all Labels
available in the section.

### Selecting Time or Date Range

The query metrics that appear in {{ qan }} are computed based on a time period or a
range of dates. The default value is *the last hour*. To set another range use
the *range selection tool* located at the top of the {{ qan }} page.

The tool consists of two parts. The *Quick ranges* offers frequently used time
ranges.. The date picker sets a range of dates.

## Totals of the Query Summary

The first line of the query summary contains the totals of the *load*, *count*,
and *latency* for all queries that were run on the selected database server
during the time period that you’ve specified.

The *load* is the amount of time that the database server spent during the
selected time or date range running all queries.

The *count* is the average number of requests to the server during the specified
time or date range.

The *latency* is the average amount of time that it took the database server to
retrieve and return the data.

## Queries in the Query Summary Table

Each row in the query summary contains information about a single
query. Each column is query attribute. The *Query* attribute informs the type of
query, such as INSERT, or UPDATE, and the queried tables, or collections. The
*ID* attribute is a unique hexadecimal number associated with the given query.

The *Load*, *Count*, and *Latency* attributes refer to the essential metrics of
each query. Their values are plotted graphics and summary values in the numeric
form. The summary values have two parts. The average value of the metric and its
percentage with respect to the corresponding total value at the top of the query
summary table.

## Viewing a Specific Value of a Metric

If you hover the cursor over one of the metrics in a query, you can see a
concrete value at the point where your cursor is located. Move the cursor along
the plotted line to watch how the value is changing.
