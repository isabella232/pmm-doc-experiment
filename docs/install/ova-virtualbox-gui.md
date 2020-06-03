# VirtualBox Using the GUI

The following procedure describes how to run the {{ pmm_server }} appliance
using the graphical user interface of VirtualBox:


1. Download the OVA. The latest version is available at the [Download Percona Monitoring and Management](https://www.percona.com/downloads/pmm) site.


2. Import the appliance. For this, open the {{ gui_file }} menu and click
{{ gui_import_appliance }} and specify the path to the OVA and click
{{ gui_continue }}. Then, select
{{ gui_reinitialize_mac_address_of_all_network_cards }} and click {{ gui_import }}.


3. Configure network settings to make the appliance accessible
from other hosts in your network.

**NOTE**: All database hosts must be in the same network as *PMM Server*,
so do not set the network adapter to NAT.

If you are running the appliance on a host with properly configured network
settings, select {{ gui_bridged_adapter }} in the {{ gui_network }} section of the
appliance settings.


4. Start the {{ pmm_server }} appliance.

If it was assigned an IP address on the network by {{ dhcp }}, the URL for
accessing {{ pmm }} will be printed in the console window.
