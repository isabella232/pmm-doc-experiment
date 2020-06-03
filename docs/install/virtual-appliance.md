# PMM Server as a Virtual Appliance

Percona provides a *virtual appliance* for running {{ pmm_server }} in a virtual
machine.  It is distributed as an *Open Virtual Appliance* (OVA) package, which
is a **tar** archive with necessary files that follow the *Open
Virtualization Format* (OVF).  OVF is supported by most popular virtualization
platforms, including:


* [VMware - ESXi 6.5](https://www.vmware.com/products/esxi-and-esx.html)


* [Red Hat Virtualization](https://www.redhat.com/en/technologies/virtualization)


* [VirtualBox](https://www.virtualbox.org/)


* [XenServer](https://www.xenserver.org/)


* [Microsoft System Center Virtual Machine Manager](https://www.microsoft.com/en-us/cloud-platform/system-center)

{{ chapter_toc }}

[TOC]

## [Supported Platforms for Running the PMM Server Virtual Appliance](virtual-appliance.md#pmm-deploying-server-virtual-appliance-supported-platform-virtual-appliance)

The virtual appliance is ideal for running {{ pmm_server }} on an enterprise
virtualization platform of your choice. This page explains how to run the
appliance in {{ virtualbox }} and VMware Workstation Player. which is a good choice
to experiment with {{ pmm }} at a smaller scale on a local machine.  Similar
procedure should work for other platforms (including enterprise deployments on
VMware ESXi, for example), but additional steps may be required.

The virtual machine used for the appliance runs {{ centos }} 7.

!!! warning
    The appliance must run in a network with DHCP, which will automatically assign an IP address for it.

To assign a static IP manually, you need to acquire the root access as
described in pmm.deploying.server.virtual-appliance.root-password.setting.
Then, see the documentation for the operating system for further
instructions: [Configuring network interfaces in CentOS](https://www.centos.org/docs/5/html/Deployment_Guide-en-US/s1-networkscripts-interfaces.html)

### Instructions for setting up the virtual machine for different platforms

## [Identifying PMM Server IP Address](virtual-appliance.md#pmm-deploying-server-virtual-appliance-pmm-server-ip-address-identifying)

When run {{ pmm_server }} as virtual appliance, The IP address of your {{ pmm_server }}
appears at the top of the screen above the login prompt. Use this address to
acces the web interface of {{ pmm_server }}.

{{ pmm_server }} uses DHCP for security reasons, and thus you need to check the PMM
Server console in order to identify the address.  If you require configuration
of a static IP address, see
[Configuring network interfaces in CentOS](https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-configure-centos-7-network-settings/)

<!-- id 9a96a76 -->
## [Accessing PMM Server](virtual-appliance.md#deploying-pmm-server-web-interface-opening)

To run the {{ pmm_server }}, start the virtual machine and open in your browser the
URL that appears at the top of the terminal when you are logging in to the
virtual machine.

If you run {{ pmm_server }} in your browser for the first time, you are requested to
supply the user login and password. The default PMM Server credentials are:


* **username:** admin


* **password:** admin

After login you will be proposed to change this default password. Enter the new
password twice and click {{ gui_save }}. The {{ pmm_server }} is now ready and the home
page opens.

You are creating a username and password that will be used for two purposes:


1. authentication as a user to PMM - this will be the credentials you need in order
to log in to PMM.


2. authentication between PMM Server and PMM Clients - you will
re-use these credentials as a part of the server URL when configuring {{ pmm_client }} for the first time on a server:

{{ tip_run_this_root }}

```
pmm-admin config --server-insecure-tls --server-url=https://admin:admin@<IP Address>:443
```

## [Accessing the Virtual Machine](virtual-appliance.md#pmm-deploying-server-virtual-appliance-accessing)

To access the VM with the *PMM Server* appliance via SSH, you will need to
provide your public key:


1. Open the URL for accessing {{ pmm }} in a web browser.

The URL is provided either in the console window or in the appliance log.


2. Select the {{ pmm_settings }} dashboard in the main menu.


3. Submit your **public key** in the *SSH Key Details* section and click the
*Apply SSH Key* button.

After that you can use `ssh` to log in as the `admin` user.
For example, if *PMM Server* is running at 192.168.100.1
and your **private key** is `~/.ssh/pmm-admin.key`,
use the following command:

```
ssh admin@192.168.100.1 -i ~/.ssh/pmm-admin.key
```

## Next Steps

Verify that PMM Server is running
by connecting to the PMM web interface using the IP address
assigned to the virtual appliance,
then install PMM Client
on all database hosts that you want to monitor.
