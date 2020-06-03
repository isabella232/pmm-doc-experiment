# Verifying PMM Server

In your browser, go to the server by its IP address. If you run your server as a
virtual appliance or by using an {{ amazon }} machine image, you will need to setup
the user name, password and your public key if you intend to connect to the
server by using ssh. This step is not needed if you run {{ pmm_server }} using
{{ docker }}.

In the given example, you would need to direct your browser to
*http://192.168.100.1*. Since you have not added any monitoring services yet,
the site will show only data related to the PMM Server internal services.

# Accessing the Components of the Web Interface

| URL                             | Component
|---------------------------------|----------------------------------------------------------
| `http://192.168.100.1`          | [PMM Home Page](/glossary-terminology.md#pmm-home-page)
| `http://192.168.100.1/graph/`   | [Metrics Monitor (MM)](/glossary-terminology.md#id17)
| `http://192.168.100.1/swagger/` | [PMM API browser](/manage/server-pmm-api)

{{ pmm_server }} provides user access control, and therefore you will need
user credentials to access it:

The default user name is `admin`, and the default password is `admin` also.
You will be proposed to change the default password at login if you didn’t it.

!!! note
    You will use the same credentials at [connecting](https://www.percona.com/doc/percona-monitoring-and-management/2.x/manage/client-config.html) your {{ pmm_client }} to {{ pmm_server }}.
