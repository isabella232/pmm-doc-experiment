# {{ stt }}

The {{ stt }} runs regular checks against connected databases,
alerting you if any servers pose a potential security threat.

The checks are automatically downloaded from {{ percona_platform }}
and run every 24 hours. (This period is not configurable.)

They run on the {{ pmm_client }} side with the results passed to {{ pmm_server }}
for display in the Failed Checks dashboard.

## How to enable {{ stt }}

{{ stt }} is disabled by default. It can be enabled in
PMM ‣ PMM Settings
(see PMM Settings Page).

## Where to see the results of checks

On your {{ pmm }} home page, the Failed security checks dashboard
shows a count of the number of failed checks.

More details can be seen by opening the Failed Checks dashboard
using PMM ‣ PMM Database Checks.

**NOTE**: After activating {{ stt }}, you must wait 24 hours
for data to appear in the dashboard.

## Checks made by {{ stt }}

<!-- The range of checks can be classified as -->
<!-- - :ref:`Generic <stt-generic-checks>`, affecting all database types; -->
<!-- - :ref:`Specific <stt-specific-checks>`, specific to a particular vendor. -->
<!-- .. _stt-generic-checks: -->
<!-- ================================================================================
Generic checks
================================================================================

+------------------------------+-----------------------------------------------+
| Check                        | Description                                   |
+==============================+===============================================+
| Latest version               | Check server software is the latest version.  |
+------------------------------+-----------------------------------------------+
| CVE                          | Check whether any CVEs are assigned to the    |
|                              | software.                                     |
+------------------------------+-----------------------------------------------+
| Password                     | Check for empty/blank passwords or default    |
|                              | passwords.                                    |
+------------------------------+-----------------------------------------------+ -->
<!-- .. _stt-specific-checks: -->
<!-- ================================================================================
Database-specific checks
================================================================================ -->
| Name

 | Description

 |
| ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |  |  |  |  |  |  |
| `mongodb_version`

                                   | Warn if MongoDB/PSMDB version is not the
latest.

                                                                                                                                                                                        |
| `mysql_empty_password`

                              | Warn if there are users without passwords.

                                                                                                                                                                                              |
| `mysql_version`

                                     | Warn if MySQL/PS/MariaDB version is not the
latest.

                                                                                                                                                                                     |
| `postgresql_version`

                                | Warn if PostgreSQL version is not the latest.

                                                                                                                                                                                           |
