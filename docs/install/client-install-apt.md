# Installing DEB packages using apt-get

If you are running a DEB-based {{ linux }} distribution, use the {{ apt }} package
manager to install {{ pmm_client }} from the official Percona software repository.

{{ percona }} provides `.deb` packages for 64-bit versions of the following
distributions:


* Debian 8 (jessie)


* Debian 9 (stretch)


* Ubuntu 14.04 LTS (Trusty Tahr)


* Ubuntu 16.04 LTS (Xenial Xerus)


* Ubuntu 16.10 (Yakkety Yak)


* Ubuntu 17.10 (Artful Aardvark)


* Ubuntu 18.04 (Bionic Beaver)

**NOTE**: {{ pmm_client }} should work on other DEB-based distributions, but it is tested
only on the platforms listed above.

To install the {{ pmm_client }} package, complete the following
procedure. {{ tip_run_all_root }}:


1. Configure {{ percona }} repositories using the [percona-release](https://www.percona.com/doc/percona-repo-config/percona-release.html) tool. First you’ll need to download and install the official percona-release package from Percona:

```
wget https://repo.percona.com/apt/percona-release_latest.generic_all.deb
sudo dpkg -i percona-release_latest.generic_all.deb
```

<script id="asciicast-LaIiFlGWZdWAMPf4p4OUEHrjB" src="https://asciinema.org/a/LaIiFlGWZdWAMPf4p4OUEHrjB.js" async data-theme="solarized-light" data-rows="8"></script>**NOTE**: If you have previously enabled the experimental or testing
Percona repository, don’t forget to disable them and enable the release
component of the original repository as follows:

```
sudo percona-release disable all
sudo percona-release enable original release
```

See [percona-release official documentation](https://www.percona.com/doc/percona-repo-config/percona-release.html) for details.


2. Install the `pmm2-client` package:

```
sudo apt-get update
sudo apt-get install pmm2-client
```

<script id="asciicast-ZBfCORUanwrZMPD3hkiHYKBkv" src="https://asciinema.org/a/ZBfCORUanwrZMPD3hkiHYKBkv.js" async data-theme="solarized-light" data-rows="8"></script>
3. Once PMM Client is installed, run the `pmm-admin config` command with your PMM Server IP address to register your Node within the Server:

```
pmm-admin config --server-insecure-tls --server-url=https://admin:admin@<IP Address>:443
```

You should see the following:

```
Checking local pmm-agent status...
pmm-agent is running.
Registering pmm-agent on PMM Server...
Registered.
Configuration file /usr/local/percona/pmm-agent.yaml updated.
Reloading pmm-agent configuration...
Configuration reloaded.
```
