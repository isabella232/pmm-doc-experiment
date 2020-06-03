# MongoDB

## Passing SSL parameters to the mongodb monitoring service

SSL/TLS related parameters are passed to an SSL enabled {{ mongodb }} server as
monitoring service parameters along with the {{ pmm_admin_add }} command when adding
the MongoDB monitoring service.

{{ tip_run_this_root }}

```
$ pmm-admin add mongodb -- --mongodb.tls
```

## Supported SSL/TLS Parameters

| Parameter                                         | Description
|---------------------------------------------------|-------------------------------------------
| {{ opt_mongodb_tls }}                             | Enable a TLS connection with mongo server
| {{ opt_mongodb_tls_ca }}  *string*                | A path to a PEM file that contains the CAs that are trusted for server connections. *If provided*: MongoDB servers connecting to should present a certificate signed by one of these CAs. *If not provided*: System default CAs are used.
| {{ opt_mongodb_tls_cert }} *string*               | A path to a PEM file that contains the certificate and, optionally, the private key in the PEM format.
This should include the whole certificate chain. *If provided*: The connection will be opened via TLS to the {{ mongodb }} server.
| {{ opt_mongodb_tls_disable_hostname_validation }} | Do hostname validation for the server connection.
| {{ opt_mongodb_tls_private_key }} *string*        | A path to a PEM file that contains the private key (if not contained in the `mongodb.tls-cert` file).

                                                                                                                                     |
```
$ mongod --dbpath=DATABASEDIR --profile 2 --slowms 200 --rateLimit 100
```
