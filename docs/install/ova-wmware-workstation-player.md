# VMware Workstation Player

The following procedure describes how to run the *PMM Server* appliance
using VMware Workstation Player:


1. Download the OVA. The latest version is available at the [Download Percona Monitoring and Management](https://www.percona.com/downloads/pmm) site.


2. Import the appliance.


    1. Open the {{ gui_file }} menu and click {{ gui_open }}.


    2. Specify the path to the OVA and click {{ gui_continue }}.

**NOTE**: You may get an error indicating that import failed.
Simply click {{ gui_retry }} and import should succeed.


3. Configure network settings to make the appliance accessible
from other hosts in your network.

If you are running the applianoce on a host
with properly configured network settings,
select **Bridged** in the **Network connection** section
of the appliance settings.


4. Start the {{ pmm_server }} appliance.

If it was assigned an IP address on the network by DHCP,
the URL for accessing PMM will be printed in the console window.
