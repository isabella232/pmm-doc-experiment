# Configuring MySQL 8.0 for PMM

{{ mysql }} 8 (in version 8.0.4) changes the way clients are authenticated by
default. The {{ opt_default_authentication_plugin }} parameter is set to
`caching_sha2_password`. This change of the default value implies that {{ mysql }}
drivers must support the SHA-256 authentication. Also, the communication channel
with {{ mysql }} 8 must be encrypted when using `caching_sha2_password`.

The {{ mysql }} driver used with {{ pmm }} does not yet support the SHA-256 authentication.

With currently supported versions of {{ mysql }}, {{ pmm }} requires that a dedicated {{ mysql }}
user be set up. This {{ mysql }} user should be authenticated using the
`mysql_native_password` plugin.  Although {{ mysql }} is configured to support SSL
clients, connections to {{ mysql }} Server are not encrypted.

There are two workarounds to be able to add {{ mysql }} Server version 8.0.4
or higher as a monitoring service to {{ pmm }}:


1. Alter the {{ mysql }} user that you plan to use with {{ pmm }}


2. Change the global {{ mysql }} configuration

### Altering the {{ mysql }} User

Provided you have already created the {{ mysql }} user that you plan to use
with {{ pmm }}, alter this user as follows:

Then, pass this user to `pmm-admin add` as the value of the `--username`
parameter.

This is a preferred approach as it only weakens the security of one user.

### Changing the global {{ mysql }} Configuration

A less secure approach is to set {{ opt_default_authentication_plugin }}
to the value **mysql_native_password** before adding it as a
monitoring service. Then, restart your {{ mysql }} Server to apply this
change.
