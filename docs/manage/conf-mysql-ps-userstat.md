# MySQL User Statistics (userstat)

User statistics is a feature of {{ percona_server }} and {{ mariadb }}.  It provides
information about user activity, individual table and index access.  In some
cases, collecting user statistics can lead to high overhead, so use this feature
sparingly.

To enable user statistics, set the {{ opt_userstat }} variable to `1`.
