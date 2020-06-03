# Understanding Top 10

<a
  id="another-doc-version-link"
  data-location="https://www.percona.com/doc/percona-monitoring-and-management/qan.html#pmm-qan-home-page-opening"
  href="https://www.percona.com/doc/percona-monitoring-and-management/2.x/qan-top-ten.html"
  style="display:none;"
></a>By default, {{ qan }} shows the top *ten* queries. You can sort queries by any
column - just click the small arrow to the right of the column name.
Also you can add a column for each additional field which is exposed by the
data source by clicking the `+` sign on the right edge of the header and
typing or selecting from the available list of fields.

To view more queries, use buttons below the query summary table.

## Query Detail Section [pmm.qan.query.selecting]

In addition to the metrics in the query metrics summary table,
**QAN** displays more information about the query itself below the table.

*Tables* tab for the selected query seen in the same section contains the table
definition and indexes for each table referenced by the query:
